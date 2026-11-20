# Préparation opérationnelle face au risque feux de forêt en Gironde (Saison 2027)

Projet d'architecture et de modélisation décisionnelle pour la préparation opérationnelle de la saison estivale 2027 face au risque accru d'incendies de forêt en Gironde, à destination de la Direction départementale du SDIS 33.

* Établissement : HETIC, Promotion Master MD5 (2026-2027)
* Modules : UE01.A Modélisation et pipelines de données & Définition des KPI et DataViz décisionnelle
* Enseignante : Marine PROST
* Certification : Titre RNCP 36209 Niveau 7, Expert en transformation digitale et technologique (Compétence CC2.1)
* Commanditaire : Direction départementale du SDIS 33 (Gironde, Nouvelle-Aquitaine)
* Livrable maître : `docs/specification.md` (Jalon cible taggué `spec-v1`)

---

## 1. État d'avancement du projet (Point d'étape au 19 novembre 2026)

Le projet est entré dans sa phase de consolidation finale pour le premier jalon officiel (`spec-v1`) :

* Cadrage stratégique et gouvernance (100 % finalisé) : Les besoins opérationnels du SDIS 33, les 6 questions de décision (Q1 à Q6), le glossaire des 13 termes canoniques et la synthèse des 6 arbitrages techniques (DEC-001 à DEC-006) sont validés et intégrés sur `dev` (Pull Request #37).
* Architecture technique et modélisation (100 % finalisé) : La stratégie d'historisation temporelle (SCD type 2 et millésimes), le pipeline 6 couches Medallion, le schéma visuel Mermaid (`docs/architecture.md`) et le planning des 5 jalons jusqu'au 11 décembre sont validés et intégrés sur `dev` (Pull Request #38).
* Qualité des données et conformité RGPD (Rédigé, en cours d'intégration) : Le profilage de l'échantillon Gironde 2022, les trois barrières de qualité automatisées (R1 complétude valeur, R2 complétude population, R3 validité physique) et la conformité RGPD par minimisation sont prêts sur la branche de rôle dédiée (`feature/spec-qualite-youssef-elhajji`).
* Sources et cohérence (Rédigé, en cours d'intégration) : L'inventaire des 4 sources retenues, les sources de référence par domaine, la matrice des manques et les règles de transformation des incohérences réelles sont prêts sur la branche de rôle dédiée (`feature/spec-sources-omar`).
* Objectif immédiat (Dimanche 22 novembre) : Fusionner les deux dernières contributions sur `dev`, exécuter la checklist de vérification, fusionner `dev` dans `main` et poser le tag `spec-v1`.
* Prochaine étape (Décembre 2026) : Implémentation du warehouse DuckDB (`feux_foret.duckdb`), calcul des indicateurs de performance (matrice de confusion, proxy météo 2022) et restitution sous forme de dashboard interactif Streamlit pour la soutenance du 11 décembre.

---

## 2. Composition de l'équipe et gouvernance

Le projet est mené par une équipe de 4 ingénieurs data, avec une séparation stricte des responsabilités par rôle et des revues de code croisées obligatoires :

| Membre | Rôle officiel | Périmètre de responsabilité | Identifiant GitHub | Branche de travail |
| :--- | :--- | :--- | :--- | :--- |
| **Ayoub AZACRI** | Chef de projet | Cadrage décisionnel, coordination du dépôt, tickets GitHub, journal des décisions, glossaire | [@Ayoub-Azacri](https://github.com/Ayoub-Azacri) | `feature/spec-cadrage-ayoub` |
| **Omar HAKIK** | Responsable sources | Inventaire des sources, fiches d'identité, sources de référence, matrice de confrontation, incohérences réelles | [@OmarHAKIK](https://github.com/OmarHAKIK) | `feature/spec-sources-omar` |
| **Youssef EL HAJJI** | Responsable qualité et conformité | Conformité RGPD, filtrage des textes libres, profilage BDIFF 2022, barrières de test de qualité (Quality Gate) | [@Youssefelhajji49](https://github.com/Youssefelhajji49) | `feature/spec-qualite-youssef-elhajji` |
| **Youssef DEKHAIL** | Responsable pipeline et modèle | Historisation (millésimes et SCD2), architecture médaillon 6 couches, schéma Mermaid, planning de livraison | [@Narodk1](https://github.com/Narodk1) | `feature/spec-pipeline-youssef-dekhail` |

---

## 3. Cartographie des documents (Où trouver quel document)

Tous les livrables d'ingénierie et d'analyse sont documentés dans le répertoire `docs/` selon une arborescence claire :

| Document | Chemin relatif | Rôle et contenu | Sections servies |
| :--- | :--- | :--- | :--- |
| **Spécification d'architecture** | [docs/specification.md](docs/specification.md) | **Livrable maître unifié.** Regroupe l'intégralité des 14 sections requises pour le jalon `spec-v1` (décision, questions, sources, manques, RGPD, historisation, qualité, architecture, contraintes, planning, glossaire, limites). | Sections 1 à 14 |
| **Schéma d'architecture technique** | [docs/architecture.md](docs/architecture.md) | Schéma visuel Mermaid formalisant le flux des données à travers les 6 couches médaillons (Sources, Brutes, Nettoyées, Consolidées, Prêtes pour analyse, Restitution) avec justification des outils (DuckDB, Parquet, Streamlit). | Section 10 |
| **Journal des décisions** | [docs/journal-des-decisions.md](docs/journal-des-decisions.md) | Registre formel des 6 arbitrages techniques et renoncements assumés (décisions DEC-001 à DEC-006) avec date, auteur, motivation métier, coût analytique et biais assumé. | Sections 5 et 14 |
| **Matrice de confrontation** | [docs/sources/matrice.md](docs/sources/matrice.md) | Tableau exhaustif croisant les 6 questions décisionnelles avec les 4 sources retenues, identifiant les lacunes de couverture et renvoyant aux décisions DEC-001 à DEC-006. | Section 5 |
| **Glossaire métier officiel** | [docs/glossaire.md](docs/glossaire.md) | Répertoire des 13 termes canoniques du domaine feux et secours (BDIFF, DFCI, Dispositif renforcé, Éclosion, Fausse alerte, IFM, Météo des forêts, Millésime, WUI) avec définitions et règles d'arbitrage. | Section 13 |
| **Fiche BDIFF** | [docs/sources/fiche-bdiff.md](docs/sources/fiche-bdiff.md) | Fiche d'identité de la Base de Données sur les Incendies de Forêt en France (IGN / Ministère Agriculture). | Sections 3, 4, 9 |
| **Fiche Météo des forêts** | [docs/sources/fiche-meteo-des-forets.md](docs/sources/fiche-meteo-des-forets.md) | Fiche d'identité des archives de vigilance prévisionnelle incendie (Météo-France). | Sections 3, 4, 9 |
| **Fiche BD Forêt V2** | [docs/sources/fiche-bd-foret.md](docs/sources/fiche-bd-foret.md) | Fiche d'identité de la cartographie surfacique des essences et combustibles végétaux (IGN). | Sections 3, 4, 9 |
| **Fiche Stations météo** | [docs/sources/fiche-stations-meteo.md](docs/sources/fiche-stations-meteo.md) | Fiche d'identité des 31 stations terrestres horaires de Gironde avec drapeaux qualité (Météo-France). | Sections 3, 4, 9 |
| **Données brutes persistées** | `data/raw/` (local) | Répertoire local contenant les archives brutes immuables téléchargées (`.csv`, `.csv.gz`, `.shp`), exclu du suivi Git via `.gitignore` pour préserver la légèreté du dépôt. | Section 11 |

---

## 4. Stratégie et utilisation des branches Git

Pour garantir une traçabilité rigoureuse et respecter les exigences d'ingénierie du Titre RNCP Niveau 7, le projet applique un cycle Gitflow strict sans aucun commit direct sur les branches protégées.

### Rôle des branches

* **`main` (Production et releases officielles) :** Branche protégée représentant les livrables stables validés. Aucun commit direct n'y est autorisé. Elle ne reçoit que des fusions issues de `dev` lors des jalons officiels, chaque livraison étant figée par un tag Git immuable (`spec-v1`, `warehouse-v1`, `release-v1`).
* **`dev` (Intégration continue de l'équipe) :** Tronc commun d'intégration collective. Toutes les Pull Requests de fonctionnalités ou de documentation ciblent obligatoirement `dev`. C'est l'espace où les contributions des 4 membres sont assemblées, testées et harmonisées avant d'être promues sur `main`.
* **Branches de fonctionnalités et de rôles (`feature/<sujet>-<nom>`) :** Chaque membre développe ses sections ou ses modules techniques sur une branche isolée créée à partir de `dev` :
  * `feature/spec-cadrage-ayoub` : Sections 1, 2, 13, 14 (Ayoub AZACRI)
  * `feature/spec-sources-omar` : Sections 3, 4, 5, 6 (Omar HAKIK)
  * `feature/spec-qualite-youssef-elhajji` : Sections 7, 9, 11 (Youssef EL HAJJI)
  * `feature/spec-pipeline-youssef-dekhail` : Sections 8, 10, 12 et `docs/architecture.md` (Youssef DEKHAIL)

### Cycle de vie d'une contribution

1. **Ticket GitHub préalable :** Toute tâche est d'abord formalisée dans un ticket avec critères d'acceptation clairs.
2. **Commits atomiques et sémantiques :** Chaque modification donne lieu à un commit ciblé respectant la convention Conventional Commits et citant explicitement le ticket :
   * Exemples : `docs(spec): add section 1 decision framing (#23)`, `docs(spec): add section 7 GDPR compliance (#25)`.
3. **Pull Request et relecture croisée obligatoire :** Le contributeur ouvre une Pull Request vers `dev`. Une revue par les pairs est systématiquement requise avant toute fusion :
   * Les sections de cadrage (Ayoub) sont relues par Youssef DEKHAIL.
   * Les sections de pipeline et modèle (Youssef D.) sont relues par Ayoub AZACRI.
   * Les sections de qualité (Youssef El H.) sont relues par Omar HAKIK.
   * Les sections de sources (Omar) sont relues par Youssef EL HAJJI.
4. **Vérification pré-fusion :** Contrôle de non-régression, vérification de l'absence de conflits, puis fusion sur `dev`.

---

## 5. Architecture technique et couches de données (Medallion pattern)

La chaîne de traitement est conçue selon une architecture médaillon à 6 couches garantissant autonomie hors-ligne, reproductibilité intégrale et gratuité des outils :

```
Sources ouvertes ───────► Données brutes (Bronze) ───────► Données nettoyées (Silver 1)
(BDIFF, Météo-France,     (data/raw/ immuable,              (Normalisation UTC, typage,
 IGN, Data.gouv.fr)        exclue du suivi Git)              contrôles qualité Pytest)
                                                                     │
                                                                     ▼
Tableau de bord Streamlit ◄─── Prêtes pour analyse (Gold) ◄─── Consolidées (Silver 2)
(Restitution SDIS 33,           (Vues SQL agrégées,            (Warehouse DuckDB, modèle
 seuils, cartographie)           matrices de confusion)         en étoile Insee x Stations)
```

1. **Sources :** Données ouvertes téléchargées via API publique ou flux WFS (BDIFF, Météo-France, IGN).
2. **Données brutes (Bronze) :** Persistance locale des fichiers originaux dans `data/raw/` pour garantir qu'aucun re-téléchargement n'est requis en cas de coupure réseau.
3. **Données nettoyées (Silver 1) :** Standardisation des dates en ISO 8601 UTC, conversion des unités de vent en km/h, gestion des valeurs manquantes (`"Inconnue"`), et validation par barrière de qualité Pytest.
4. **Données consolidées (Silver 2 / Warehouse) :** Modèle dimensionnel en étoile sous moteur **DuckDB** (`feux_foret.duckdb`) croisant feux, météo et combustible végétal au grain communal Insee et horaire.
5. **Données prêtes pour l'analyse (Gold) :** Vues SQL matérialisant les matrices de confusion de la Météo des forêts et les profils micro-climatiques.
6. **Restitution :** Application interactive Streamlit permettant aux officiers du SDIS 33 de simuler l'impact des seuils d'alerte et d'optimiser le pré-positionnement des moyens de secours.

---

## 6. Citations des sources, licences et droits de reproduction

L'ensemble des données mobilisées dans ce projet d'aide à la décision pour le SDIS 33 est documenté avec leurs licences respectives et respecte une séparation stricte entre données brutes et données dérivées :

* **Base de Données sur les Incendies de Forêts en France (BDIFF) :** Produite par l'IGN et le Ministère de l'Agriculture et de la Souveraineté alimentaire. Données ouvertes sous Licence Ouverte v2.0 (Etalab).
* **Archives de la Météo des forêts (2024–2026) :** Produite par Météo-France. Données ouvertes sous Licence Ouverte v2.0 (Etalab).
* **Données climatologiques horaires des 31 stations de Gironde (2022–2026) :** Produite par Météo-France via la plateforme meteo.data.gouv.fr. Données publiques Météo-France.
* **BD Forêt V2 :** Produite par l'IGN (Institut national de l'information géographique et forestière). Données ouvertes sous Licence Ouverte v2.0 (Etalab).

### Mentions légales et données dérivées

1. **Cadre d'usage académique et non commercial :** Ce projet est réalisé à des fins d'ingénierie et de recherche appliquée pour le commandement opérationnel du SDIS 33 dans le cadre du Titre RNCP 36209 Niveau 7 (HETIC Master MD5). Les données ne sont ni vendues, ni louées, ni soumises à redevance, et excluent toute finalité commerciale ou publicitaire.
2. **Statut de données dérivées :** Les tables nettoyées, les modèles analytiques sous DuckDB et les tableaux de bord de restitution sont présentés comme des **données dérivées réalisées à partir des sources officielles**, et non comme les données des sources elles-mêmes.
3. **Respect de l'intégrité et droits réservés :** La couche Bronze (`data/raw/`) préserve l'intégrité intégrale des données sources sans altération. Les droits de reproduction et de diffusion des données sources demeurent réservés et strictement limités à leurs producteurs officiels.
Pour le détail technique de chaque source et des consignes d'ingestion, se référer au guide [data/README.md](data/README.md).
