# Architecture technique du pipeline décisionnel - SDIS 33

* Auteur : Youssef DEKHAIL (Responsable pipeline et modèle)
* Binôme d'architecture : Ayoub AZACRI (Chef de projet)
* Date : 18 novembre 2026
* Référence projet : Section 10 de la spécification (`docs/specification.md`), ticket #32
* Objectif : Modéliser le flux complet de transformation des données depuis les sources Open Data brutes jusqu'aux indicateurs d'aide à la décision opérationnelle pour la saison feux 2027.

---

## 1. Schéma d'architecture des 6 couches

```mermaid
flowchart TD
    subgraph C1 ["Couche 1 : Sources externes"]
        S_BDIFF["BDIFF (IGN / Ministère Agriculture)<br/>Export CSV & Flux WFS"]
        S_MDF["Météo des forêts (Météo-France)<br/>Archives CSV.GZ S3"]
        S_FORET["BD Forêt V2 (IGN)<br/>Extraction Shapefile / WFS D033"]
        S_METEO["Stations horaires (Météo-France)<br/>Archives CSV.GZ S3 Gironde"]
    end

    subgraph C2 ["Couche 2 : Données brutes (Raw)"]
        R_BDIFF["data/raw/echantillon_bdiff_gironde_2022.csv<br/>Immuable"]
        R_MDF["data/raw/mdf_2024.csv.gz<br/>Immuable"]
        R_FORET["data/raw/echantillon_bdforet_gironde.geojson<br/>Immuable"]
        R_METEO["data/raw/H_33_previous-2020-2024.csv.gz<br/>Immuable"]
    end

    subgraph C3 ["Couche 3 : Données nettoyées (Clean)"]
        CL_BDIFF["clean_bdiff<br/>Dates ISO 8601 UTC, code Insee 5 car.<br/>Surfaces positives"]
        CL_MDF["clean_meteo_forets<br/>Niveaux entiers 1 à 4, dates ISO<br/>Filtre Gironde 33"]
        CL_FORET["clean_occupation_sol<br/>Taux enrésinement communal<br/>Code Insee, essence Pin maritime"]
        CL_METEO["clean_stations_meteo<br/>Projection 8 colonnes utiles, T, FF, U<br/>Filtre drapeaux qualité = 1"]
        QG["Barrière de qualité (Pytest)<br/>Tests automatisés sur les types et bornes"]
    end

    subgraph C4 ["Couche 4 : Entrepôt consolidé (Warehouse)"]
        DIM_COMMUNE["dim_commune<br/>code_insee PK, nom, massif_dfci,<br/>taux_pin_maritime"]
        DIM_STATION["dim_station_meteo<br/>num_poste PK, nom, lat, lon, alti"]
        FAIT_FEU["fait_incendie<br/>id_incendie PK, date_alerte, heure,<br/>code_insee FK, surface_brulee_ha"]
        FAIT_VIGILANCE["fait_vigilance_mdf<br/>date PK, num_dep PK, niveau_j1, niveau_j2"]
        FAIT_METEO["fait_releve_horaire<br/>num_poste FK, date_heure PK, T, FF, FXY, U"]
    end

    subgraph C5 ["Couche 5 : Données prêtes pour analyse (Analytics)"]
        V_CONFUSION["vue_matrice_confusion<br/>Croisement MDF x Feux réels (2024-2026)<br/>Taux de fausses alertes et oublis"]
        V_MASSIFS["vue_risque_massif<br/>Départs de feux x Taux pin x Mois<br/>Calibration seuil par secteur DFCI"]
        V_ANOMALIES["vue_anomalies_vert_jaune<br/>Feux sous vigilance faible x Rafales FXY,<br/>Chute humidité U"]
        V_BENCHMARK["vue_benchmark_regional<br/>Surface moyenne par feu Gironde vs NA vs France"]
    end

    subgraph C6 ["Couche 6 : Restitution décisionnelle"]
        DASH_SEUILS["Grille opérationnelle de déclenchement 2027<br/>Aide à la décision CTA-CODIS"]
        DASH_CARTES["Cartographie du risque par massif<br/>Pré-positionnement des moyens CCF / GIFF"]
        DASH_ASTREINTES["Planning d'astreintes temporelles<br/>Dimensionnement par créneau horaire"]
    end

    S_BDIFF --> R_BDIFF
    S_MDF --> R_MDF
    S_FORET --> R_FORET
    S_METEO --> R_METEO

    R_BDIFF --> CL_BDIFF
    R_MDF --> CL_MDF
    R_FORET --> CL_FORET
    R_METEO --> CL_METEO

    CL_BDIFF --> QG
    CL_MDF --> QG
    CL_FORET --> QG
    CL_METEO --> QG

    QG --> DIM_COMMUNE
    QG --> DIM_STATION
    QG --> FAIT_FEU
    QG --> FAIT_VIGILANCE
    QG --> FAIT_METEO

    DIM_COMMUNE --> V_CONFUSION
    FAIT_FEU --> V_CONFUSION
    FAIT_VIGILANCE --> V_CONFUSION

    DIM_COMMUNE --> V_MASSIFS
    FAIT_FEU --> V_MASSIFS
    FAIT_METEO --> V_MASSIFS

    FAIT_FEU --> V_ANOMALIES
    FAIT_VIGILANCE --> V_ANOMALIES
    FAIT_METEO --> V_ANOMALIES

    FAIT_FEU --> V_BENCHMARK

    V_CONFUSION --> DASH_SEUILS
    V_MASSIFS --> DASH_CARTES
    V_ANOMALIES --> DASH_SEUILS
    V_BENCHMARK --> DASH_CARTES
    FAIT_FEU --> DASH_ASTREINTES
```

---

## 2. Description détaillée des 6 couches

### Couche 1 : Sources externes
* **Rôle :** Plateformes officielles de diffusion en Open Data des données publiques.
* **Composants :** Portail data.gouv.fr (BDIFF, Archives Météo des forêts, Données horaires de base Météo-France) et Géoplateforme IGN (BD Forêt V2).
* **Mode de collecte :** Téléchargements HTTP directs et requêtes d'extraction WFS pour les emprises géographiques ciblées.

### Couche 2 : Données brutes (Raw Data)
* **Rôle :** Zone d'atterrissage locale immuable. Les fichiers sont stockés sous leur forme native dans le répertoire `data/raw/`.
* **Règle de gestion :** Aucun fichier brut n'est altéré ni versionné sur Git (exclus via `.gitignore` pour préserver la légèreté du dépôt). Les données sont consultables hors-ligne pour garantir la reproductibilité totale sans dépendance réseau.

### Couche 3 : Données nettoyées (Clean Data)
* **Rôle :** Normalisation technique et application stricte du principe de minimisation.
* **Transformations :**
  1. *Standardisation temporelle :* Conversion de tous les horodatages en format ISO 8601 UTC (`YYYY-MM-DDTHH:MM:SSZ`).
  2. *Standardisation spatiale :* Formatage des codes Insee communaux sur 5 caractères avec zéro initial.
  3. *Projection colonne :* Réduction des 206 colonnes brutes des stations météo à 8 colonnes utiles (`NUM_POSTE`, `AAAAMMJJHH`, `T`, `FF`, `FXY`, `DD`, `U`, `RR1`).
  4. *Agrégation spatiale :* Extraction du pourcentage de couverture en pin maritime par commune à partir de la BD Forêt V2, sans conserver la géométrie polygonale lourde.
* **Barrière de qualité (Quality Gate) :** Validation automatisée par tests Pytest vérifiant la complétude (`id_incendie IS NOT NULL`), la validité physique (`surface >= 0`, `T <= 55 °C`) et les drapeaux de mesure (`Q = 1`).

### Couche 4 : Entrepôt de données consolidé (Warehouse)
* **Rôle :** Modèle dimensionnel en étoile sous moteur DuckDB, optimisé pour les requêtes analytiques rapides.
* **Schéma relationnel :**
  * *Tables de dimensions :* `dim_commune` (caractéristiques territoriales et taux d'enrésinement), `dim_station_meteo` (coordonnées et altitude des capteurs).
  * *Tables de faits :* `fait_incendie` (sinistres BDIFF validés), `fait_vigilance_mdf` (niveaux prévisionnels J+1/J+2), `fait_releve_horaire` (conditions atmosphériques physiques).
* **Clés de liaison :** Jointures relationnelles sur `code_insee`, `date` et couple (`NUM_POSTE`, `date_heure`).

### Couche 5 : Données prêtes pour l'analyse (Analytics / Datamart)
* **Rôle :** Vues SQL et tables dérivées directement exploitables pour répondre aux questions décisionnelles.
* **Vues spécialisées :**
  * `vue_matrice_confusion` : Décompte des vrais positifs, faux positifs, vrais négatifs et faux négatifs pour évaluer la pertinence de chaque couleur d'alerte.
  * `vue_risque_massif` : Taux de sinistralité par massif forestier DFCI et par mois pour guider la modulation géographique.
  * `vue_anomalies_vert_jaune` : Isolement des conditions de vent et d'hygrométrie lors des feux survenus sous indice faible.
  * `vue_benchmark_regional` : Surface moyenne par feu par département.

### Couche 6 : Restitution décisionnelle (Delivery)
* **Rôle :** Outils d'aide à la décision pour le commanditaire (SDIS 33).
* **Livrables :** Tableaux de bord de simulation du seuil optimal, cartographies des massifs prioritaires pour les rondes estivales, et calendrier hebdomadaire/horaire pour le dimensionnement des gardes postées.
