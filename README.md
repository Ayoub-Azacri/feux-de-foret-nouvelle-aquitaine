# feux-de-foret-nouvelle-aquitaine

Projet d'architecture et de modélisation décisionnelle pour la préparation opérationnelle de la saison estivale 2027 face au risque accru de feux de forêt en Gironde, à destination de la Direction du SDIS 33.

---

## 1. Contexte académique et professionnel

* **Établissement :** HETIC - Promotion MD5 (2026-2027)
* **Module :** UE01.A Modélisation et pipelines de données
* **Enseignante :** Marine PROST
* **Certification visée :** Titre RNCP 36209 Niveau 7 - Expert en transformation digitale et technologique (Compétence CC2.1)
* **Commanditaire :** Direction départementale du SDIS 33 (Gironde, Nouvelle-Aquitaine)
* **Livrable maître de phase :** `docs/specification.md` (Version cible taggée `spec-v1`)

---

## 2. Gouvernance et répartition des rôles

| Rôle | Responsabilités | Membre | Identifiant GitHub | Branche dédiée |
| :--- | :--- | :--- | :--- | :--- |
| **Chef de projet** | Cadrage décisionnel, gouvernance, synthèse du journal des décisions | Ayoub AZACRI | `@Ayoub-Azacri` | `feature/spec-cadrage-ayoub` |
| **Responsable sources** | Inventaire, fiches d'identité, matrice de confrontation, incohérences réelles | Omar HAKIK | `@OmarHAKIK` | `feature/spec-sources-omar` |
| **Responsable qualité et conformité** | Conformité RGPD, profilage de l'échantillon 2022, barrière de qualité (Quality Gate) | Youssef EL HAJJI | `@Youssefelhajji49` | `feature/spec-qualite-youssef-elhajji` |
| **Responsable pipeline et modèle** | Historisation temporelle, architecture 6 couches (schéma Mermaid), jalons de livraison | Youssef DEKHAIL | `@Narodk1` | `feature/spec-pipeline-youssef-dekhail` |

---

## 3. Table d'orientation des livrables (Map of Content)

Ce dépôt centralise l'ensemble de la démarche d'ingénierie et des arbitrages opérationnels :

* **[Spécification d'architecture (docs/specification.md)](docs/specification.md) :** Document maître unifié regroupant les 14 sections requises pour le jalon `spec-v1`.
* **[Schéma d'architecture (docs/architecture.md)](docs/architecture.md) :** Schéma visuel Mermaid formalisant le flux des données à travers les 6 couches médaillons.
* **[Journal des décisions (docs/journal-des-decisions.md)](docs/journal-des-decisions.md) :** Registre formel des arbitrages techniques et renoncements assumés (décisions DEC-001 à DEC-006).
* **[Matrice de confrontation (docs/sources/matrice.md)](docs/sources/matrice.md) :** Croisement exhaustif des 6 questions de décision avec les 4 sources retenues et identification des manques.
* **[Glossaire métier officiel (docs/glossaire.md)](docs/glossaire.md) :** Répertoire des 13 termes canoniques SDIS 33 (DFCI, éclosion, IFM, vigilance Météo des forêts, WUI).
* **[Fiches d'identité des sources (docs/sources/)](docs/sources/) :**
  * `docs/sources/fiche-bdiff.md` : Base de Données sur les Incendies de Forêt en France (IGN / Ministère Agriculture).
  * `docs/sources/fiche-meteo-des-forets.md` : Archives de la vigilance prévisionnelle Météo-France.
  * `docs/sources/fiche-bd-foret.md` : Inventaire forestier national et cartographie des essences (IGN).
  * `docs/sources/fiche-stations-meteo.md` : Relevés horaires terrestres instrumentaux (Météo-France).

---

## 4. Organisation de l'architecture en couches (Medallion pattern)

Le pipeline de données est structuré en 6 couches conformes au standard Data Lakehouse :

1. **Sources :** Connecteurs d'ingestion des flux ouverts et fichiers bruts (HTTP / WFS).
2. **Données brutes (Bronze) :** Persistance immutable et horodatée dans `data/raw/` (exclue de Git par `.gitignore`).
3. **Données nettoyées (Silver 1) :** Standardisation des formats (ISO 8601 UTC), conversion des unités (km/h) et typage strict.
4. **Données consolidées (Silver 2) :** Jointure spatio-temporelle unifiée au grain communal Insee et horaire sous DuckDB.
5. **Données prêtes pour l'analyse (Gold) :** Tables agrégées pour matrices de confusion et dimensionnement des gardes.
6. **Restitution :** Tableaux de bord interactifs et simulateur de seuils sous Streamlit pour le commanditaire.

---

## 5. Protocole Gitflow et livraison

* Tronc commun d'intégration : branche `dev`.
* Chaque membre travaille sur une branche dédiée, réalise un commit atomique par section, et ouvre une Pull Request vers `dev`.
* Version finale de livraison : Pull Request de `dev` vers `main`, puis pose du tag officiel :
  ```bash
  git tag spec-v1
  git push origin spec-v1
  ```
