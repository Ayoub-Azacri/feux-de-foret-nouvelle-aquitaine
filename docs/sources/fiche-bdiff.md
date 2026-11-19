# Fiche d'identité de source : Base de Données sur les Incendies de Forêts en France (BDIFF)

* Auteur de la fiche : Ayoub AZACRI
* Rôle : Chef de projet
* Date d'exploration : 17 novembre 2026
* URL de la source : https://bdiff.agriculture.gouv.fr/incendies
* Référence catalogue data.gouv.fr : https://www.data.gouv.fr/datasets/base-de-donnees-sur-les-incendies-de-forets-en-france-bdiff

## 1. Caractéristiques techniques et administratives

| Rubrique | Valeur constatée et vérifiée |
| :--- | :--- |
| **Propriétaire et système** | Ministère de l'Agriculture et de la Souveraineté Alimentaire, en coordination avec le Ministère de l'Intérieur. Opérateur technique délégué : Institut national de l'information géographique et forestière (IGN). Système source : BDIFF, application nationale alimentée par les déclarations des services de secours (SDIS), de l'ONF et des directions départementales des territoires (DDTM). |
| **Mode d'accès et format** | Téléchargement direct depuis le formulaire web filtré de la BDIFF. Formats disponibles : export tabulaire CSV (encodage UTF-8) et flux géographique WFS sur la Géoplateforme IGN (data.geopf.fr). Fichier testé et inspecté localement : echantillon_bdiff_gironde_2022.csv. |
| **Grain (une ligne = ?)** | Un événement d'incendie de forêt déclaré, instruit et validé par les autorités publiques, identifié par un numéro de fiche unique (ex. 2022-11533). |
| **Emprise géographique** | France métropolitaine intégrale (96 départements). L'échantillon extrait en local est filtré sur le département de la Gironde (33). |
| **Période réellement couverte** | Données archivées de 2006 à 2024. Le fichier local de validation couvre la totalité de la saison 2022 en Gironde. |
| **Date de dernière mise à jour affichée** | 2 mai 2022 sur la notice data.gouv.fr. Le portail ministériel bdiff.agriculture.gouv.fr fait l'objet d'une alimentation continue lors des campagnes annuelles de consolidation. |
| **Fréquence de mise à jour** | Annuelle pour la validation juridique des bilans de feux ; saisie au fil de l'eau en cours de saison par les unités instructrices. |
| **Volumétrie** | Environ 60 000 à 80 000 lignes pour l'historique national depuis 2006 (ordre de grandeur de 20 à 40 Mo). Pour la Gironde sur l'année de crise 2022 : 245 lignes recensées dans le fichier officiel (environ 25 Ko). |
| **Clés disponibles** | Clés primaires et jointures vérifiées : id_incendie (identifiant unique de la fiche), code_insee (code commune Insee sur 5 caractères, ex. 33248 pour Listrac-Médoc), date_heure_alerte (horodatage à la minute du premier appel), code_departement (33). Coordonnées GPS précises (latitude et longitude en degrés décimaux) : non vérifiée dans cet export tabulaire brut (seul le chef-lieu communal et le code Insee sont explicités dans le CSV ; la géométrie surfacique requiert le flux WFS). |
| **Données personnelles** | Aucune donnée personnelle (conformité RGPD par conception). Les données sont strictement matérielles : date, surface, nature générale de la cause constatée. Aucun nom, numéro de téléphone, matricule d'agent ou adresse privée n'est présent. |
| **Licence** | Licence Ouverte v2.0 (Etalab). Réutilisation libre et gratuite sous réserve de mentionner la paternité de la source. Licence non contaminante : compatible avec l'intégration dans tout entrepôt décisionnel sans obligation de redistribution copyleft ODbL. |
| **Questions de votre analyse couvertes** | Question 1 (complète) : identification des communes et massifs girondins à forte récurrence d'éclosion. Question 2 (partielle) : fournit la réalité terrain des feux réels, à croiser avec l'indice Météo-France. Question 3 (complète sur la surface finale, partielle sur la cinétique minute par minute) : benchmark de la sévérité moyenne par feu entre départements. Question 4 (complète) : analyse de la répartition hebdomadaire et horaire des alertes pour calibrer les astreintes. |

## 2. Analyse critique et retour d'expérience terrain

### Apports concrets pour les arbitrages du SDIS 33
La BDIFF constitue la source de référence étatique pour mesurer la réalité des feux en Gironde. Elle fournit deux variables fondamentales pour la direction des secours : la date avec heure de première alerte, et la ventilation des surfaces brûlées (forêt, autres terres boisées, terres non boisées). Ces champs permettent d'isoler les départs de feux réels des fausses alertes signalées au centre de traitement de l'alerte (CTA-CODIS).

### Limites et anomalies constatées dans les données réelles
L'inspection du fichier extrait révèle deux contraintes majeures :
* Forte proportion de causes non renseignées : la colonne nature_cause présente une majorité de mentions « Inconnue » (ex. 7 feux sur les 10 premières lignes de l'échantillon 2022). La qualification de la cause humaine (négligence, mégot, travaux forestiers, malveillance) n'est consolidée qu'après enquête judiciaire, ce qui limite son usage en temps réel.
* Absence de géométrie vectorielle dans l'export tabulaire : le fichier CSV fournit le code Insee de la commune mais ne donne pas les coordonnées GPS précises du point d'éclosion ni le polygone de contour du feu. Pour cartographier finement l'aléa le long des pistes DFCI, un croisement avec les référentiels de l'IGN ou le flux WFS sera nécessaire.

### Verdict d'exploitabilité pour le projet
Source validée et hautement exploitable. Elle servira de table de faits centrale dans l'entrepôt pour quantifier les départs de feux réels et mesurer la performance du seuil Météo des forêts.
