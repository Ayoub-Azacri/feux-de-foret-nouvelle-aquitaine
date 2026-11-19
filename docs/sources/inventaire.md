# Inventaire des sources : prévention et détection des feux de forêt (Gironde)

* Document consolidé par : Omar HAKIK (Responsable sources)
* Relecture et validation : Ayoub AZACRI (Chef de projet)
* Date : 17 novembre 2026
* Contexte : UE01.A Modélisation et pipelines de données (SDIS 33, saison feux 2027)

## 1. Tableau synthétique des sources explorées

| Source | Explorée par | Pertinente pour nos questions ? | Ce que nous avons découvert |
| :--- | :--- | :--- | :--- |
| **BDIFF (Base de Données sur les Incendies de Forêts en France)** | Ayoub AZACRI (Chef de projet) | Oui, hautement pertinente (table de faits centrale). | Historique national officiel de 2006 à 2024 (245 feux recensés en Gironde en 2022). Fournit la date et l'heure du premier appel à la minute près, ainsi que la ventilation des surfaces brûlées (forêt, autres terres). Limites : coordonnées GPS non renseignées dans l'export tabulaire brut (nécessite le flux WFS pour la géométrie fine) et cause humaine majoritairement classée en « Inconnue ». |
| **Archives de la Météo des forêts (Météo-France)** | Omar HAKIK (Responsable sources) | Oui, directement pertinente pour l'évaluation des seuils d'alerte. | Niveaux de vigilance prévus à J+1 et J+2 (de 1: Vert à 4: Rouge) par département. Fichier très léger et propre (11 520 lignes/an au niveau national, 120 lignes pour la Gironde par saison estivale). Limites : historique court limité aux saisons 2024 à 2026 (aucun historique open data pour l'été de crise 2022) et granularité départementale uniforme masquant les disparités locales entre la côte atlantique, les massifs forestiers et le vignoble. |
| **BD Forêt® V2 (IGN)** | Youssef DEKHAIL (Responsable pipeline et modèle) | Oui, indispensable pour la modélisation spatiale du combustible forestier. | Cartographie vectorielle fine des formations végétales dès 0,5 hectare, permettant d'isoler les peuplements inflammables de pin maritime face aux feuillus et aux interfaces avec le bâti. Limites : décalage temporel critique (prises de vue aériennes de 2012-2015 publiées en 2017 ne reflétant pas les plus de 30 000 hectares détruits en 2022), absence de code Insee direct (nécessite une jointure géospatiale SIG) et volumétrie vectorielle très lourde (> 200 Mo). |
| **Données climatologiques de base horaires (Météo-France)** | Youssef EL HAJJI (Responsable qualité et conformité) | Oui, pertinente comme vérité terrain physique (vent et température). | Relevés physiques horaires sur 31 stations terrestres en Gironde (861 911 lignes sur la période 2020-2024). Permet de reconstituer les conditions atmosphériques réelles de vent (FF, FXY), température (T) et humidité (U) lors des journées d'alerte. Limites : forte hétérogénéité d'équipement entre stations (ex. la station Belin-Béliet 1 ne mesure ni le vent ni l'humidité), table large de 206 colonnes avec beaucoup de valeurs nulles, et obligation de filtrer sur les drapeaux de contrôle qualité (Q...). |

## 2. Bilan critique de l'inventaire

### Quelles questions de vos analyses n'ont encore aucune source ?
Deux volets majeurs de la commande du SDIS 33 restent aujourd'hui sans couverture dans les catalogues Open Data :
* Les données budgétaires et financières internes du SDIS 33 : le montant de l'enveloppe allouée pour la saison 2027 et le coût financier réel d'une journée de mobilisation renforcée (rémunération des gardes postées, carburant des patrouilles, maintenance des engins de lutte). Ces données relèvent de la comptabilité de gestion interne des pompiers et ne sont pas publiques.
* Le protocole opérationnel exact du seuil de déclenchement : la valeur officielle et le texte de doctrine qui régissent aujourd'hui l'activation du dispositif renforcé en Gironde (déclenchement systématique dès l'indice Orange ou réservé au niveau Rouge, règles d'exception locales des chefs de centre).
* Les données d'engagement opérationnel à la minute : effectifs réels déployés par caserne, nombre de véhicules engagés et délais de présentation sur les lieux lors des éclosions de feux.

### Quelle source vous a surpris, et pourquoi ?
Deux sources nous ont surpris par leurs contraintes temporelles inattendues :
* La BD Forêt V2 de l'IGN nous a surpris par son décalage temporel (effet millésime) : la version de référence pour la Gironde repose sur des campagnes de photos aériennes de 2012 à 2015. Elle ignore donc totalement les destructions massives des incendies historiques de 2022 (Landiras et La Teste-de-Buch, plus de 30 000 hectares brûlés) et de 2026. L'utiliser brute reviendrait à considérer comme du pin maritime dense des zones aujourd'hui rasées ou en régénération.
* Les Archives de la Météo des forêts nous ont surpris par leur absence d'historique : le dispositif national de vigilance n'ayant été inauguré qu'en juin 2023, aucun historique Open Data n'est disponible pour la saison de référence 2022. Pour évaluer la pertinence de l'indice lors de cette crise, le groupe devra croiser la BDIFF avec les données physiques des stations horaires ou reconstituer l'indice à partir du code IFM.

### Quelle source semble utile mais inexploitable dans le temps du projet ?
La BD Forêt V2 dans son format vectoriel complet (Shapefile ou GeoPackage de plus de 200 Mo, comprenant plusieurs dizaines de milliers de polygones géographiques). Bien qu'essentielle pour qualifier le combustible, son exploitation vectorielle brute exigerait des calculs d'intersections géospatiales (spatial joins) beaucoup trop longs et complexes pour un pipeline décisionnel classique dans les délais impartis.

Décision retenue par l'équipe : nous renonçons à ingérer le maillage vectoriel fin polygone par polygone. Nous allons approximer le facteur combustible en effectuant une extraction préalable agrégée à l'échelle communale (pourcentage de couverture en pin maritime par code Insee communal) afin d'alimenter une dimension territoriale simple et légère dans l'entrepôt.
