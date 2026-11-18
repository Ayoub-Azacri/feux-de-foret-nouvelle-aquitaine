# Spécification d'architecture : Préparation opérationnelle de la saison feux 2027 (SDIS 33)

Groupe : Ayoub AZACRI (Chef de projet), Omar HAKIK (Responsable sources), Youssef EL HAJJI (Responsable qualité et conformité), Youssef DEKHAIL (Responsable pipeline et modèle) · Version du 18 novembre 2026 (Tag cible : spec-v1)

---

## 1. La décision

<!-- Section 1 : Attribuée à Ayoub AZACRI (Ticket #23 - Branche feature/spec-cadrage-ayoub) -->

Le Service Départemental d'Incendie et de Secours de la Gironde (SDIS 33) prépare son dispositif opérationnel estival face au risque accru de feux de forêt pour la saison estivale 2027. La décision consiste à calibrer le dimensionnement préventif des gardes postées en caserne, l'ordonnancement des patrouilles de surveillance de massifs et le seuil de déclenchement du dispositif renforcé. Ce cadrage opérationnel doit être validé d'ici mai 2027 pour engager les arrêtés préfectoraux et la planification des astreintes des sapeurs-pompiers.

---

## 2. Les questions retenues

<!-- Section 2 : Attribuée à Ayoub AZACRI (Ticket #23 - Branche feature/spec-cadrage-ayoub) -->

| N° | Question | Décision qu'elle éclaire | Proposée par |
| :--- | :--- | :--- | :--- |
| **Q1** | Concentration spatiale des éclosions et massifs vulnérables | Identifier les communes et massifs à fort risque pour cibler les patrouilles | Ayoub, Omar, Youssef EL H., Youssef D. |
| **Q2** | Fiabilité du seuil Météo des forêts et matrice de confusion | Calibrer objectivement le niveau d'alerte pour réduire les fausses alertes | Ayoub, Omar, Youssef EL H., Youssef D. |
| **Q3** | Modulation spatiale (massifs) et temporelle (mois) du seuil d'alerte | Différencier le déclenchement entre Landes de Gascogne, littoral et vignoble | Youssef D., Ayoub |
| **Q4** | Départs de feu non anticipés sous vigilance faible ou modérée (Vert / Jaune) | Évaluer la vulnérabilité micro-climatique et adapter la posture de garde | Omar, Youssef EL H. |
| **Q5** | Comparaison interdépartementale de la surface moyenne brûlée par feu | Benchmark régional face aux Landes (40) et à la zone Méditerranée | Ayoub, Omar, Youssef EL H., Youssef D. |
| **Q6** | Ventilation horaire et hebdomadaire pour les astreintes pompiers | Dimensionner les vacations et les gardes postées en caserne par tranche de 2h | Ayoub |

Questions écartées, avec la raison et le renvoi au journal :
* Calcul de la cinétique horaire fine de propagation en hectares par heure (ha/h) : écartée car la BDIFF ne contient pas l'heure de maîtrise du feu (renvoi DEC-005).
* Calcul du coût financier analytique direct en euros des gardes pompiers : écartée car les données comptables internes du SDIS 33 ne sont pas publiques ; remplacée par un paramètre forfaitaire indicatif (renvoi DEC-006).

---

## 3. Les sources retenues

<!-- Section 3 : Attribuée à Omar HAKIK (Ticket #24 - Branche feature/spec-sources-omar) -->

*Tableau des 4 sources retenues (avec lien vers les fiches d'identité, colonnes utiles, questions servies) et sources écartées.*

---

## 4. Les sources de référence

<!-- Section 4 : Attribuée à Omar HAKIK (Ticket #24 - Branche feature/spec-sources-omar) -->

*Tableau de la source d'autorité unique par domaine partagé (incendies, météo prévisionnelle, végétation, mesures physiques).*

---

## 5. Les manques

<!-- Section 5 : Attribuée à Omar HAKIK (Ticket #24 - Branche feature/spec-sources-omar) -->

*Tableau des manques issus de docs/sources/matrice.md reliés aux décisions d'arbitrage (DEC-001 à DEC-006) et coûts analytiques.*

---

## 6. Les incohérences repérées et les transformations nécessaires

<!-- Section 6 : Attribuée à Omar HAKIK (Ticket #24 - Branche feature/spec-sources-omar) -->

*Tableau des incohérences réelles de format (dates, codes spatiaux, unités de vent) et transformations prévues.*

---

## 7. Conformité

<!-- Section 7 : Attribuée à Youssef EL HAJJI (Ticket #25 - Branche feature/spec-qualite-youssef-elhajji) -->

*Analyse RGPD par champ, filtrage des textes libres et évaluation du risque de ré-identification.*

---

## 8. Historisation

<!-- Section 8 : Attribuée à Youssef DEKHAIL (Ticket #26 - Branche feature/spec-pipeline-youssef-dekhail) -->

La gestion de la dérive temporelle, des millésimes de référence et des séries chronologiques hétérogènes constitue un enjeu central pour la fiabilité du pipeline décisionnel du SDIS 33.

### 8.1. BD Forêt V2 : figeage du millésime de référence et correction post-incendies
* **Millésime de référence fové :** Les données vectorielles de la BD Forêt V2 pour la Gironde reposent sur la campagne de photographies aériennes de 2012-2015 publiées en 2017. L'entrepôt fige cette source comme référentiel spatial historique de base (`millesime = 2017`).
* **Correction des communes sinistrées en 2022 :** Cette couverture ignorant les destructions des méga-feux de juillet et août 2022 (Landiras et La Teste-de-Buch, plus de 30 000 hectares brûlés) et de l'été 2026, le pipeline applique une recalibration d'éclosion. Les surfaces forestières réellement actives sont corrigées au niveau communal en soustrayant les surfaces calcinées consolidées dans la BDIFF, évitant de surévaluer le combustible disponible dans les zones déjà brûlées ou en coupe sanitaire.

### 8.2. Météo des forêts : partitionnement annuel et estival
* **Période de diffusion :** L'indice officiel de la Météo des forêts est publié exclusivement lors de la campagne estivale (du 1er juin au 30 septembre) depuis l'été 2024.
* **Règle de partitionnement :** Les tables de faits de vigilance sont partitionnées par année et par campagne estivale (`annee`, `mois`). Chaque campagne annuelle constitue un jeu de données autonome et immuable.
* **Traitement de la rupture 2022 :** En l'absence d'historique officiel pour la saison de crise 2022, un seuil proxy physique est simulé via les stations météo horaires (température > 35 °C, vent moyen > 30 km/h, humidité relative < 30%) conformément à la décision DEC-002, tracé sous le statut `source = 'proxy_physique_reconstitue'`.

### 8.3. Stations horaires : figeage de l'archive et append des flux récents
* **Figeage de l'archive décennale :** Le fichier d'archive 2020-2024 (`H_33_previous-2020-2024.csv.gz`) est figé en zone de données nettoyées comme socle d'apprentissage et de calibrage historique.
* **Alimentation incrémentale (Append-Only) :** Les relevés récents des saisons 2025 et 2026 sont intégrés par chargement incrémental régulier (mode append) sans réécrire l'historique consolidé, garantissant des temps de traitement optimaux.

### 8.4. Découpage administratif Insee et gestion des fusions communales
* **Rattachement au COG d'origine :** Les feux de la BDIFF sont rattachés au Code Officiel Géographique (COG) en vigueur lors de l'année du sinistre.
* **Alignement décisionnel 2027 :** Pour la restitution opérationnelle destinée aux officiers du SDIS 33, une table de passage Insee projette l'ensemble des historiques sur la nomenclature communale active au 1er janvier 2027 (gestion de type SCD 1 sur la dimension communale pour refléter les fusions récentes sans fausser les décomptes passés).

---

## 9. Entrées attendues et qualité

<!-- Section 9 : Attribuée à Youssef EL HAJJI (Ticket #25 - Branche feature/spec-qualite-youssef-elhajji) -->

*Exigences par source, profilage réel de l'échantillon Gironde 2022 et 3 règles de test automatisées (quality gate).*

---

## 10. Architecture

<!-- Section 10 : Attribuée à Youssef DEKHAIL (Ticket #26 - Branche feature/spec-pipeline-youssef-dekhail) -->

Le pipeline décisionnel s'articule autour de 6 couches logiques normalisées, garantissant la traçabilité des transformations et la conformité aux exigences de l'enseignante.

Le schéma d'architecture complet avec les flux de composants et le diagramme Mermaid est documenté dans le fichier compagnon [`docs/architecture.md`](architecture.md).

### Tableau des 6 couches du pipeline

| N° | Couche | Format et stockage | Responsabilité technique | Questions servies (Q1 à Q6) |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Sources** | Portails data.gouv.fr et Géoplateforme IGN (CSV, CSV.GZ, WFS) | Flux bruts CSV, .csv.gz, GeoJSON interrogés par requêtes HTTP ou scripts d'ingestion depuis les producteurs officiels (IGN, Météo-France, Ministère de l'Agriculture). | Socle d'autorité pour l'ensemble des questions Q1 à Q6. |
| **2** | **Données brutes (Raw)** | Répertoire local `data/raw/` (fichiers natifs immuables non versionnés) | Stockage immuable dans `data/raw/` avec horodatage de collecte, garantissant la persistance brute et la reproductibilité hors-ligne sans dépendance réseau. | Traçabilité intégrale pour l'auditabilité RNCP. |
| **3** | **Données nettoyées (Clean)** | Vues ou tables DuckDB / fichiers Parquet typés | Standardisation UTC, typage rigoureux, formatage des codes Insee, projection stricte sur 8 colonnes météo (minimisation) et validation par la barrière de qualité Pytest. | Q2 (fiabilité des seuils sans valeurs erronées), Q4 (anomalies météo vérifiées), Q6 (créneaux horaires propres). |
| **4** | **Données consolidées (Warehouse)** | Modèle dimensionnel en étoile sous moteur DuckDB (`feux_foret.duckdb`) | Jointure spatio-temporelle Insee x Station x Feux sous DuckDB reliant les tables de dimensions (`dim_commune`, `dim_station_meteo`) et de faits (`fait_incendie`, `fait_vigilance_mdf`, `fait_releve_horaire`). | Q1 (concentration massifs), Q3 (modulation spatiale), Q5 (benchmark départemental de surface brûlée). |
| **5** | **Données prêtes pour l'analyse (Analytics)** | Vues SQL et tables dérivées d'agrégation | Tables agrégées pour matrices de confusion (taux de fausses alertes et de non-détections), indicateurs de sinistralité par massif et par mois, et profils horaires d'éclosion. | Q2 (matrice de confusion officielle), Q3 (seuils optimaux par secteur DFCI), Q4 (anomalies sous vigilance Vert/Jaune), Q5 (surface moyenne détruite). |
| **6** | **Restitution** | Interface interactive (Streamlit / tableaux de bord décisionnels) | Visualisations interactives Streamlit pour le SDIS 33 restituant la grille de déclenchement 2027, la cartographie des massifs prioritaires et le planning des astreintes. | Support direct aux deux décisions stratégiques de la direction du SDIS 33. |

---

## 11. Contraintes

<!-- Section 11 : Attribuée à Youssef EL HAJJI (Ticket #25 - Branche feature/spec-qualite-youssef-elhajji) -->

*Respect des contraintes opérationnelles (outils gratuits, persistance brute, autonomie hors-ligne, données incomplètes).*

---

## 12. Planning de réalisation

<!-- Section 12 : Attribuée à Youssef DEKHAIL (Ticket #26 - Branche feature/spec-pipeline-youssef-dekhail) -->

Le déploiement du pipeline décisionnel respecte un séquencement itératif rigoureux en 5 jalons successifs. Conformément aux consignes de cours, chaque jalon est validé par une preuve technique tangible et vérifiable.

### Séquencement chronologique et preuves de validation

| Jalon | Intitulé de la phase | Contenu technique et livrables | Échéance | Preuve formelle vérifiable |
| :--- | :--- | :--- | :--- | :--- |
| **Jalon 1** | **Ingestion et persistance brute** | Scripts d'ingestion brute dans `data/raw/` (BDIFF, Météo des forêts, BD Forêt V2, Stations horaires) et figeage des extraits locaux. | 24 nov. 2026 | Fichiers bruts présents dans `data/raw/`, script d'ingestion exécutable sans erreur et PR fusionnée dans `dev`. |
| **Jalon 2** | **Nettoyage et barrière de qualité** | Standardisation UTC, typage, projection colonnes et implémentation des règles de quality gate avec Pytest. | 27 nov. 2026 | Suite de tests automatisés Pytest passant avec succès (code retour 0) et tag Git officiel `clean-v1`. |
| **Jalon 3** | **Consolidation spatio-temporelle DuckDB** | Modélisation en étoile (`dim_...` et `fait_...`), jointures spatio-temporelles Insee x Station x Feux sous DuckDB. | 01 déc. 2026 | Base de données locale `feux_foret.duckdb` générée via script SQL/CLI unique et tag Git `warehouse-v1`. |
| **Jalon 4** | **Tables d'analyse et indicateurs de confusion** | Vues analytiques d'agrégation, calcul de la matrice de confusion 2024-2026, proxy météo 2022 et benchmark régional. | 04 déc. 2026 | Requêtes SQL analytiques de validation produisant les résultats chiffrés pour les 6 questions décisionnelles. |
| **Jalon 5** | **Dashboard Streamlit et finalisation soutenance** | Application interactive Streamlit pour le SDIS 33, rapport final d'architecture et répétition de la soutenance. | 08 déc. 2026 | Démonstration opérationnelle du dashboard validée pour la soutenance du 11 décembre 2026 et tag final `release-v1` sur `main`. |

### Hypothèses techniques d'ordonnancement
1. **Autonomie locale hors-ligne :** Tous les scripts de traitement fonctionnent à partir des extraits bruts locaux persistés dans `data/raw/`, éliminant tout blocage lié aux limites de requêtes (rate limiting) ou à l'indisponibilité temporaire des API gouvernementales.
2. **Technologie légère et standard :** Le choix de DuckDB et Python élimine le besoin d'infrastructure cloud payante ou de serveurs de bases de données lourds (PostgreSQL / Oracle). L'intégralité du pipeline peut être exécutée sur n'importe quel poste de travail standard en moins de 30 secondes.
3. **Traçabilité Git continue :** Aucun commit direct n'est toléré sur `main` ni sur `dev`. Chaque évolution technique fait l'objet de la branche de rôle `feature/spec-pipeline-youssef-dekhail`, d'un commit par section (#26), d'une Pull Request relue par Youssef EL HAJJI et de tests automatisés validés avant fusion.

---

## 13. Glossaire

<!-- Section 13 : Attribuée à Ayoub AZACRI (Ticket #23 - Branche feature/spec-cadrage-ayoub) -->

Lien vers le glossaire complet : `docs/glossaire.md` · Nombre de termes : 13 termes officiels validés · Termes encore « à vérifier » : 0.

Chaque terme employé dans ce document de spécification (BDIFF, DFCI, Dispositif renforcé, Éclosion, Fausse alerte, IFM, Météo des forêts, Millésime, Taux de feux non anticipés, WUI) dispose de sa fiche complète avec définition métier, registre, divergences repérées et règle d'arbitrage formalisée dans `docs/glossaire.md`.

---

## 14. Limites connues

<!-- Section 14 : Attribuée à Ayoub AZACRI (Ticket #23 - Branche feature/spec-cadrage-ayoub) -->

Ce que cette spécification ne permettra pas de dire au commanditaire, et pourquoi :
1. Elle ne permettra pas de calculer un bilan financier réel à l'euro près des économies réalisées, en raison de l'absence de données comptables publiques sur la masse salariale et les coûts de fonctionnement du SDIS 33 (remplacé par un estimateur paramétrique forfaitaire, renvoi DEC-006).
2. Elle ne permettra pas de modéliser la vitesse de propagation fine minute par minute des fronts de flammes en hectares par heure, car la BDIFF consigne l'heure du premier appel mais pas l'heure de maîtrise ni d'extinction du sinistre (renvoi DEC-005).
3. Elle ne pourra pas prédire avec certitude les départs de feux d'origine humaine accidentelle (mégots, débroussaillage) survenus lors de journées à très faible indice de danger météorologique, le risque étant comportemental et non climatique.

### Synthèse du Journal des décisions

Lien vers le journal complet des arbitrages : `docs/journal-des-decisions.md`

| ID | Date | Auteur | Question | Nature | Motivation opérationnelle | Coût analytique et biais assumé |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **DEC-001** | 17/11/2026 | Ayoub AZACRI | Q1 | Approximer | Absence de coordonnées GPS précises dans le CSV brut BDIFF | Agrégation au niveau de la commune Insee, masquant les disparités locales internes |
| **DEC-002** | 17/11/2026 | Omar HAKIK | Q2 | Approximer | Absence d'archives Météo des forêts pour la canicule historique de 2022 | Reconstitution par un proxy physique météo (T > 35°C, vent > 30 km/h, U < 30%) |
| **DEC-003** | 17/11/2026 | Youssef DEKHAIL | Q3 | Approximer | Absence d'anémomètre et d'hygromètre sur la station forestière de Belin-Béliet | Substitution par les données de la station voisine de Cazats (à 25 km) |
| **DEC-004** | 17/11/2026 | Youssef EL HAJJI | Q4 | Approximer | Grain départemental uniforme de la vigilance masquant les micro-climats | Croisement avec les stations terrestres locales pour isoler les anomalies thermiques |
| **DEC-005** | 18/11/2026 | Ayoub AZACRI | Q5 | Renoncer | Heure d'extinction du feu absente de la BDIFF (cinétique ha/h impossible) | Renoncement à la vitesse d'expansion au profit de la surface moyenne finale détruite |
| **DEC-006** | 18/11/2026 | Ayoub AZACRI | Q6 | Approximer | Absence des données de comptabilité analytique interne du SDIS 33 | Paramétrage d'un coût forfaitaire indicatif renseigné par le commanditaire |
