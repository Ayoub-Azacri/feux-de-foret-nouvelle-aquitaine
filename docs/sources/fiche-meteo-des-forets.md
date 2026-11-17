# Fiche d'identité de source : Archives de la Météo des forêts

* Auteur de la fiche : Omar HAKIK
* Rôle : Responsable sources
* Date d'exploration : 17 novembre 2026
* URL de la source : https://www.data.gouv.fr/fr/datasets/archives-de-la-meteo-des-forets/

| Rubrique | Valeur constatée |
| :--- | :--- |
| **Propriétaire et système** | Météo-France (Direction des opérations / service national de prévention des feux de forêt). |
| **Mode d'accès et format** | Téléchargement direct de fichiers CSV compressés (`.csv.gz`) hébergés sur stockage S3 OVHcloud et API publique Météo-France. |
| **Grain (une ligne = ?)** | Une ligne représente le niveau d'alerte incendie prévu à J+1 (`niveau_j1`) et J+2 (`niveau_j2`) pour un département français à une date d'échéance donnée. |
| **Emprise géographique** | France métropolitaine entière (96 départements administratifs, incluant la Gironde - code 33). |
| **Période réellement couverte** | Fichier ouvert `mdf_2024.csv.gz` : du 03/06/2024 au 30/09/2024 (saison estivale). Des archives similaires existent pour 2024, 2025 et 2026. |
| **Date de dernière mise à jour affichée** | 9 septembre 2026 sur la fiche officielle data.gouv.fr. |
| **Fréquence de mise à jour** | Quotidienne en période estivale (juin à septembre) ; consolidation annuelle pour les fichiers d'archives CSV. |
| **Volumétrie** | 11 521 lignes au total (dont 1 ligne d'en-tête), environ 40 Ko compressé (~450 Ko décompressé). Exactement 120 lignes pour la Gironde (33). |
| **Clés disponibles** | Clé géographique : `num_dep` (code département, ex. `33`) et `nom_dep` (`Gironde`). Clé temporelle : `date` (horodatage ISO 8601 : `YYYY-MM-DDTHH:MM:SSZ`). Pas de code Insee commune ni de GPS. |
| **Données personnelles** | Non. Aucune donnée nominative, aucun identifiant personnel (100 % conforme RGPD). |
| **Licence** | Licence Ouverte / Open Licence version 2.0 (Etalab) : réutilisation libre et gratuite y compris commerciale, avec mention de paternité, non contaminante. |
| **Questions de votre analyse couvertes** | Questions 2, 3 et 4 de l'analyse individuelle (proportion de feux par couleur météo, départs sous indice vert/jaune, comparaison Gironde vs ensemble des départements français). |

## Analyse critique et observations

* **Ce que le fichier apporte concrètement pour le SDIS 33 :**  
  Permet d'évaluer objectivement la pertinence des seuils d'alerte en croisant par date (`date`) et département (`num_dep = 33`) avec les départs de feux réels de la BDIFF. Cela permet de calculer le taux de fausses alertes (jours Orange/Rouge sans intervention majeure) et le taux de feux non anticipés (feux survenus sous indice Vert/Jaune).

* **Limites ou anomalies détectées :**  
  1. *Grain géographique trop large :* L'indice est calculé uniquement à l'échelle du département entier. Il ne permet pas de distinguer le risque localement entre le massif des Landes de Gascogne au sud, le Médoc ou le vignoble bordelais.  
  2. *Absence de variables physiques directes :* Le fichier ne fournit que l'indice consolidé de 1 à 4 (1: Vert, 2: Jaune, 3: Orange, 4: Rouge). Il ne contient ni la force du vent en km/h, ni la température, ni l'humidité (il faudra croiser avec la source stations météo pour analyser le vent).  
  3. *Couverture limitée à la saison estivale :* Les relevés ne commencent qu'en juin et s'arrêtent fin septembre. Les feux de végétation de fin d'hiver ou de printemps ne sont pas documentés.

* **Verdict d'exploitabilité pour le projet :**  
  **Exploitable directement.** Le fichier est très propre, léger, sans valeurs manquantes sur les niveaux de danger, et immédiatement joignable avec l'historique des feux via le couple `(date, num_dep)`.
