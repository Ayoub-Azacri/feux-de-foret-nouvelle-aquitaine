# Gestion des données et gouvernance des sources (Couches Bronze et Silver)

Ce répertoire centralise les données du projet selon les principes de l'**architecture médaillon** et les exigences d'intégrité des sources, de licences d'exploitation et de lignage des données (*data lineage*).

---

## 1. Organisation des répertoires

```
data/
├── README.md           # Ce guide officiel de gouvernance et d'inventaire des sources
├── raw/                # COUCHE BRONZE : Données brutes immuables (exclues de Git via .gitignore)
└── processed/          # COUCHE SILVER : Données nettoyées, typées, UTC et validées par Pytest
```

### Règle d'or sur la couche Bronze (`data/raw/`)
* **Immuabilité stricte :** Les fichiers déposés dans `data/raw/` par les scripts d'ingestion proviennent directement des serveurs officiels et ne doivent **jamais** être modifiés, altérés ou renommés manuellement.
* **Interdiction de falsification :** Il est formellement interdit de corriger une date, de modifier une localisation ou de combler des valeurs manquantes directement dans un fichier brut en prétendant qu'il s'agit de la source.
* **Exclusion Git :** Les données brutes volumineuses sont exclues du suivi Git pour préserver la légèreté du dépôt. Elles sont téléchargées automatiquement par le script `src/ingestion/download_sources.py`.

### Règle d'or sur la couche Silver (`data/processed/`)
* **Données dérivées :** Toutes les transformations (typage explicite, conversion en ISO 8601 UTC, calculs de métriques combinées, traitement des valeurs nulles) sont réalisées par du code Python (`src/cleaning/clean_data.py`) qui lit la couche Bronze et écrit dans la couche Silver.
* **Conservation du lignage (*data lineage*) :** Chaque enregistrement nettoyé ou enrichi reste traçable jusqu'à sa valeur brute d'origine dans la couche Bronze.

---

## 2. Inventaire des 4 sources officielles retenues

| Source | Producteur officiel | Catalogue et URL officielle | Licence d'exploitation | Période couverte | Usage dans le projet |
|---|---|---|---|---|---|
| **BDIFF** | Ministère de l'Agriculture / IGN | [bdiff.agriculture.gouv.fr/incendies](https://bdiff.agriculture.gouv.fr/incendies) | Licence Ouverte v2.0 (Etalab) | 2022–2026 | Historique des départs de feux, surfaces brûlées (ha), communes et causes. |
| **Météo des forêts** | Météo-France | [data.gouv.fr/datasets/archives-de-la-meteo-des-forets](https://www.data.gouv.fr/fr/datasets/archives-de-la-meteo-des-forets/) | Licence Ouverte v2.0 (Etalab) | 2024–2026 | Niveaux de vigilance prévisionnels quotidiens (Vert, Jaune, Orange, Rouge). |
| **Stations météorologiques horaires** | Météo-France | [meteo.data.gouv.fr](https://meteo.data.gouv.fr) | Données publiques Météo-France | 2022–2026 (1er juin - 30 sept) | Relevés horaires des 31 stations de Gironde (température, vent, rafales, hygrométrie). |
| **BD Forêt V2** | IGN | [geoservices.ign.fr/bdforet](https://geoservices.ign.fr/bdforet) | Licence Ouverte v2.0 (Etalab) | Millésime V2 de référence | Cartographie surfacique des essences inflammables (massif de pin maritime monoculture). |

---

## 3. Cadre juridique, licences et mentions légales

Conformément aux règles de diffusion et d'utilisation des données publiques :

1. **Cadre académique et non commercial :**  
   L'utilisation de ces données s'inscrit exclusivement dans le cadre d'un projet d'ingénierie et de recherche appliquée au commandement opérationnel du SDIS 33 (Titre RNCP 36209 Niveau 7, HETIC Master MD5). Aucune utilisation commerciale ou publicitaire n'est faite de ces informations. Les données ne sont ni vendues, ni louées, ni soumises à redevance.

2. **Statut de données dérivées :**  
   Les jeux de données nettoyés, agrégés et modélisés dans l'entrepôt DuckDB (`feux_foret_nouvelle_aquitaine.duckdb`) ainsi que les visualisations associées sont présentés comme **réalisés à partir des sources officielles précitées**, et non comme les données des sources elles-mêmes.

3. **Droits de reproduction réservés :**  
   Les droits de reproduction et de diffusion des données d'origine demeurent réservés aux producteurs officiels (Météo-France, IGN, Ministère de l'Agriculture).
