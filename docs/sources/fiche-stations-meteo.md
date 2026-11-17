# Fiche d'identité de source : Données climatologiques de base horaires (Météo-France)

* Auteur de la fiche : Youssef EL HAJJI
* Rôle : Responsable qualité et conformité
* Date d'exploration : 17 novembre 2026
* URL du catalogue data.gouv.fr : https://www.data.gouv.fr/datasets/donnees-climatologiques-de-base-horaires
* Identifiant du jeu de données : 6569b4473bedf2e7abad3b72
* Portail officiel producteur : https://meteo.data.gouv.fr

## 1. Caractéristiques techniques et administratives

| Rubrique | Valeur constatée et vérifiée |
| :--- | :--- |
| **Propriétaire et système** | Météo-France (Établissement public administratif sous tutelle du Ministère de la Transition écologique). Système source : Base Climatologique Publique (BCP), alimentée par le réseau opérationnel de stations météorologiques terrestres (stations synoptiques, agro-météorologiques et thermo-pluviométriques). |
| **Mode d'accès et format** | Téléchargement direct par protocole HTTPS (stockage S3 OVH Cloud synchronisé avec le FTP Météo-France). Formats proposés : archives CSV compressées en gzip (.csv.gz) avec séparateur point-virgule et encodage UTF-8. Fichier inspecté et testé localement : H_33_previous-2020-2024.csv.gz. |
| **Grain (une ligne = ?)** | Un relevé physique horaire horodaté pour une station météorologique donnée, caractérisé par le couple NUM_POSTE et le timestamp AAAAMMJJHH en temps universel coordonné (UTC). |
| **Emprise géographique** | Département de la Gironde (33) pour le fichier ciblé, découpé à l'échelle nationale pour l'ensemble des 96 départements métropolitains. Le département 33 comprend 31 stations météorologiques actives réparties sur le territoire (Belin-Béliet, Captieux, Cazats, Lacanau, Hourtin, Cap-Ferret, Mérignac, etc.). |
| **Période réellement couverte** | Du 1er janvier 2020 à 00h00 UTC au 31 décembre 2024 à 23h00 UTC pour le fichier d'archives testé. L'historique complet disponible sur le portail remonte par tranches décennales depuis les années 1840, et un fichier distinct couvre la période temps réel 2025-2026. |
| **Date de dernière mise à jour affichée** | 3 juin 2026 sur la fiche descriptive data.gouv.fr. Les fichiers de la décennie en cours font l'objet d'un rafraîchissement régulier après validation par les contrôles qualité de Météo-France. |
| **Fréquence de mise à jour** | Mensuelle pour la consolidation définitive des données d'expertise ; flux quotidien pour le suivi en temps réel. |
| **Volumétrie** | 861 911 lignes et 206 colonnes pour le département 33 sur la période 2020-2024 (taille compressée : 14,8 Mo ; taille décompressée : environ 185 Mo). |
| **Clés disponibles** | Clés primaires et jointures vérifiées : NUM_POSTE (identifiant officiel de la station sur 8 chiffres, ex. 33042001 pour Belin-Béliet), AAAAMMJJHH (horodatage UTC au format année-mois-jour-heure), LAT et LON (coordonnées GPS de la station en WGS84 décimal), ALTI (altitude du capteur en mètres). Permet une jointure spatio-temporelle avec les incendies de la BDIFF par proximité géographique (station la plus proche du départ de feu) et par créneau horaire. |
| **Données personnelles** | Aucune donnée personnelle (conformité RGPD intégrale). Données exclusivement physiques, environnementales et instrumentales. |
| **Licence** | Licence Ouverte v2.0 (Etalab). Réutilisation gratuite pour tout usage professionnel ou public, avec obligation de citation de la paternité Météo-France. Licence non contaminante : compatible avec tout système décisionnel interne sans obligation de redistribution copyleft. |
| **Questions de votre analyse couvertes** | Question 3 (couverture partielle) : fournit les variables physiques indispensables (température, vent moyen, rafales, humidité) pour mesurer objectivement les conditions atmosphériques lors des journées d'alerte élevée sans incendie, ou lors des feux éclos sous faible vigilance. Questions 1, 2 et 4 (non couvertes) : ne contient ni la liste des départs de feux, ni l'indice synthétique d'alerte Météo des forêts, ni les statistiques territoriales comparatives. |

## 2. Analyse critique et retour d'expérience terrain

### Apports concrets pour les arbitrages du SDIS 33
Ce jeu de données constitue la référence physique incontournable pour auditer les conditions atmosphériques réelles ayant conduit aux grands incendies girondins. L'analyse fine des relevés horaires lors du départ de feu de Landiras (le 12 juillet 2022) montre la corrélation immédiate entre la flambée des températures (plus de 35 °C mesurés sous abri) et la chute brutale de l'hygrométrie relative. Ces données permettent au SDIS 33 d'expliquer pourquoi certains massifs deviennent explosifs indépendamment d'un classement départemental uniforme.

### Limites et anomalies constatées dans les données réelles
L'inspection concrète du fichier H_33_previous-2020-2024.csv.gz met en évidence trois contraintes majeures qui intéressent directement le volet qualité :
* Hétérogénéité d'équipement entre stations : sur les 31 stations recensées en Gironde, beaucoup ne disposent pas de tous les capteurs. Par exemple, la station historique de Belin-Béliet (33042001) mesure la température et la pluie mais ne dispose pas d'anémomètre ni d'hygromètre opérationnel dans cet export (valeurs de vent et d'humidité nulles pour toutes les lignes observées). Pour obtenir le vent dans ce secteur forestier critique, le pipeline devra obligatoirement sélectionner la station voisine de Cazats (33116001) ou Belin-Béliet 2 (33042005).
* Structure tabulaire très large à forte proportion de valeurs nulles : les 206 colonnes intègrent des grandeurs spécialisées (hauteur de neige, rayonnement, état du sol) qui ne sont pas mesurées en plaine girondine. Le pipeline d'ingestion devra appliquer une projection stricte sur 6 à 8 variables utiles (NUM_POSTE, AAAAMMJJHH, T, FF, FXY, U, RR1) pour éviter la surcharge mémoire.
* Règle des indicateurs de contrôle qualité : chaque mesure est accompagnée de son drapeau de contrôle (QRR1, QFF, QT, QU). Ces codes qualité exigent une règle de gestion explicite dans le pipeline : accepter les mesures validées (code 1) et rejeter ou imputer les mesures suspectes (codes 2 ou 9).

### Verdict d'exploitabilité pour le projet
Source exploitable avec prétraitement obligatoire. Bien qu'elle ne contienne pas l'indice Météo des forêts lui-même, elle apporte la vérité terrain physique nécessaire pour calibrer les seuils météorologiques du SDIS 33 et expliquer les écarts de comportement des feux.
