# Rendu cadrage technique · Groupe SDIS 33

| Rubrique | Votre réponse |
|---|---|
| **Groupe (numéro, membres)** | Groupe SDIS 33 : Ayoub AZACRI (Chef de projet), Youssef DEKHAIL, Youssef EL HAJJI, Omar HAKIK |
| **Décideur et décision** | **Le décideur :** Le Directeur départemental du SDIS 33 (Commandement opérationnel des sapeurs-pompiers de Gironde).<br>**La décision :** Réviser le seuil de déclenchement de l'alerte renforcée et adapter les plannings de garde postée sur le pic thermique 14h-18h UTC pour la saison estivale 2027. |
| **Lien GitHub** | https://github.com/Ayoub-Azacri/feux-de-foret-nouvelle-aquitaine |
| **Accès au dépôt** | Public (accès ouvert pour l'évaluation et la soutenance) |

## Sources prévues

| Source (nom exact) | Producteur | Lien | Période | Champs utilisés |
|---|---|---|---|---|
| **BDIFF (Base de Données sur les Incendies de Forêts en France)** | Ministère de l'Agriculture et de la Souveraineté alimentaire / IGN | https://bdiff.agriculture.gouv.fr/incendies | 2022–2026 | `date_premiere_alerte`, `heure_alerte`, `code_insee`, `surface_totale_brulee_ha`, `nature` (cause) |
| **Archives de la Météo des forêts** | Météo-France | https://www.data.gouv.fr/fr/datasets/archives-de-la-meteo-des-forets/ | 2024–2026 (archives officielles) | `date`, `num_dep` (33 et région Nouvelle-Aquitaine), `niveau_j` (danger jour J), `niveau_j1` (vigilance J+1) |
| **Données climatologiques de base horaires (31 stations)** | Météo-France | https://meteo.data.gouv.fr | 2022–2026 (saison estivale 1er juin - 30 sept) | `NUM_POSTE`, `AAAAMMJJHH`, `T` (température sèche °C), `U` (humidité relative %), `FF` (vitesse vent moyen), `FXI` (rafales max) |
| **BD Forêt V2** | IGN (Institut national de l'information géographique et forestière) | https://geoservices.ign.fr/bdforet | Version V2 consolidée (millésime de référence) | `code_insee`, `essence_principale` (pin maritime monoculture), `surface_boisee_ha`, `taux_resineux` |

## Outils choisis

| Usage | Outil | Pourquoi ce choix |
|---|---|---|
| **Base de données** | **DuckDB (Embedded OLAP)** | Moteur SQL analytique ultra-rapide en local. Gère le schéma en étoile (`fait_feux`, `dim_communes`, `dim_calendrier`, `dim_meteo`) sans dépendance serveur lourd. Zéro manipulation manuelle dans Excel. |
| **Dataviz** | **Streamlit (Python) & Power BI** | **Approche hybride :**<br>1. **Streamlit (Python) :** Dashboard web interactif déployé depuis le code du repo, multiplateforme (Linux/Mac/Windows), facilement versionné sous Git.<br>2. **Power BI (`.pbix`) :** Export du modèle tabulaire pour exploration décisionnelle conforme au cours. |
| **Langage / pipeline** | **Python (Pandas / Polars)** | Pipeline d'ingestion automatisé, normalisation stricte des horodatages en ISO 8601 UTC et reproductibilité intégrale de bout en bout. |
| **Autre (Qualité & Tests)** | **Pytest** | Barrières de qualité automatisées (Quality Gates) vérifiant les complétudes temporelles (122 jours estivaux sans trou) et les bornes physiques avant alimentation de la DataViz. |

## Risques identifiés

* **Données manquantes ou non ouvertes :** L'indice officiel de la Météo des forêts a été créé mi-2023 : il n'existe pas d'archive officielle MDF pour l'été 2022. Solution retenue et validée : utilisation des 31 stations météorologiques terrestres de Nouvelle-Aquitaine pour calculer un proxy physique exact (rafales > 30 km/h et hygrométrie < 30 %) sur l'historique 2022.
* **Volume ou accès :** Fichiers volumineux sur les relevés météo horaires de la région. Solution retenue : ingestion automatisée par script Python découpé par département et stockage local optimisé sous format Parquet / DuckDB.
* **Autre (Fausse complétude & Biais temporels) :** Risque d'occulter des jours sans feu ou de confondre les feux de débroussaillement d'hiver avec les feux de cime estivaux. Solution : cadrage strict sur la fenêtre estivale (1er juin au 30 septembre) et calendrier complet sans trou de 122 jours.
