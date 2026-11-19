# Diagnostic territorial et objectifs SMART (SDIS 33)

* **Commanditaire :** Direction départementale du SDIS 33 (Gironde, Nouvelle-Aquitaine)
* **Cadre académique :** HETIC Master MD5 · Module UE01.B Définition des KPI et DataViz décisionnelle
* **Enseignante :** Marine PROST
* **Certification :** Titre RNCP 36209 Niveau 7 (Compétence CC2.1)
* **Auteur :** Ayoub AZACRI (Chef de projet)
* **Ticket associé :** Issue [#40](https://github.com/Ayoub-Azacri/feux-de-foret-nouvelle-aquitaine/issues/40)
* **Branche dédiée :** `feature/kpi-objectifs-smart`
* **Relecteur officiel :** Youssef DEKHAIL (`@Narodk1`, Responsable architecture & pipeline)

---

## 1. Diagnostic de situation territoriale et retour d'expérience (2022-2026)

### Le contexte du massif girondin et le double niveau de comparaison
Le département de la Gironde (SDIS 33) abrite près de 500 000 hectares de forêt, constitués à plus de 70 % de pin maritime en monoculture intensive au sein du massif des Landes de Gascogne. Ce combustible végétal présente une inflammabilité thermique et une combustibilité exceptionnelles lors des vagues de chaleur estivales.

Conformément à la commande du Directeur départemental du SDIS 33, le diagnostic positionne la Gironde selon un double niveau de référence :
1. **Échelle régionale (Nouvelle-Aquitaine) :** La Gironde concentre à elle seule plus de 65 % des surfaces détruites par le feu en Nouvelle-Aquitaine lors des années de canicule, très loin devant les Landes (40) ou la Dordogne (24).
2. **Échelle nationale (France entière) :** Si l'arc méditerranéen (PACA, Corse, Occitanie) enregistre le plus grand nombre d'éclosions annuelles, la Gironde se caractérise par des méga-feux d'une gravité surfacique extrême : en 2022, 50 % des surfaces brûlées sur l'ensemble du territoire français l'ont été sur le seul département de la Gironde.

### Le traumatisme opérationnel de la saison 2022
La saison estivale 2022 a constitué une rupture d'échelle historique :
* Plus de 30 000 hectares de massifs ont été réduits en cendres lors des deux méga-feux simultanés de Landiras (environ 20 000 ha) et de La Teste-de-Buch (environ 7 000 ha).
* Plus de 36 000 riverains et touristes ont dû être évacués en urgence sous un dôme de chaleur dépassant les 42°C et des sautes de feu imprévisibles de plusieurs centaines de mètres.
* Le SDIS 33 a mobilisé l'intégralité de ses effectifs permanents, complétés par des colonnes de renfort extra-départementales et la flotte aérienne nationale (Canadair et Dash).

### Identification des 4 dysfonctionnements majeurs
L'analyse croisée des retours d'expérience du SDIS 33, des archives Météo-France et de la BDIFF met en lumière 4 limites structurelles :

1. **Défaillance de l'indice de vigilance prévisionnel :**  
   L'indice Météo des forêts actuel (calculé à l'échelle départementale globale) ne reflète pas les disparités micro-climatiques locales. Plusieurs départs de feux destructeurs (> 5 ha) ont éclos lors de journées classées sous vigilance basse (Vert ou Jaune). À l'inverse, des alertes de niveau Orange n'ont parfois donné lieu à aucun départ, créant un risque de démobilisation psychologique des équipes.
2. **Latence de l'attaque initiale sur parcelles isolées :**  
   En 2022, le délai moyen entre l'appel au 18/112 et l'arrivée du premier engin porteur d'eau (CCF) a atteint 18 minutes sur les secteurs reculés du Sud-Gironde. Or, la doctrine opérationnelle fixe le seuil critique d'extinction facile avant que le feu ne dépasse le premier hectare à moins de 10 minutes.
3. **Sollicitation asymétrique et dimensionnement horaire des astreintes :**  
   L'analyse historique démontre que plus de 80 % des éclosions critiques surviennent sur la plage horaire 14h00-18h00 UTC, lorsque la température est maximale, l'humidité de l'air minimale (< 30 %) et les brises thermiques actives. Le maintien d'astreintes rigides de 8h00 à 12h00 mobilise inutilement du budget sans couvrir le pic de danger.
4. **Risque de sur-réaction et loi de Goodhart :**  
   Face au traumatisme de 2022, la tentation du commandement serait d'abaisser tous les seuils d'alerte pour mobiliser les casernes en permanence. Cette sur-réaction ferait exploser le taux de fausses alertes, épuiserait les sapeurs-pompiers volontaires dès la mi-juillet et grèverait le budget de fonctionnement du SDIS.

---

## 2. Les 3 objectifs SMART opérationnels pour la saison 2027

Pour répondre au mandat du directeur départemental du SDIS 33, nous formalisons 3 objectifs SMART opérationnels. Chaque objectif est mesurable dans nos futures tables DuckDB et couplé à un garde-fou contre les effets pervers.

### Objectif SMART 1 : Fiabilisation de l'alerte précoce et calibrage du seuil critique (Questions Q2 et Q4)

* **S (Spécifique) :** Calibrer un seuil de vigilance renforcée adapté à la Gironde pour éliminer les départs de feux significatifs (> 5 ha) survenus par surprise sous vigilance annoncée basse (Vert ou Jaune).
* **M (Mesurable) :** Réduire le **Taux de feux non anticipés** à moins de 15 % sur la campagne estivale active (du 1er juin au 30 septembre 2027).  
  *Garde-fou obligatoire (Loi de Goodhart) :* Maintenir le **Taux de fausses alertes** sous le plafond strict de 35 % pour éviter l'épuisement des effectifs et la sur-mobilisation budgétaire.
* **A (Atteignable) :** Réalisable par le croisement prédictif à J+1 (`niveau_j1`) avec un correcteur d'anomalie physique locale (rafales de vent > 30 km/h et hygrométrie < 30 % issues des 31 stations terrestres).
* **R (Réaliste) :** Testé et validé par rétro-simulation SQL sur les historiques de feux 2022-2026.
* **T (Temporel) :** Algorithme de calcul opérationnel et intégré au tableau de bord d'aide à la décision avant le 15 juin 2027.

### Objectif SMART 2 : Optimisation spatiale du prépositionnement préventif (Questions Q1 et Q5)

* **S (Spécifique) :** Concentrer les patrouilles de surveillance DFCI et les groupes d'intervention feux de forêt (GIFF) sur les communes concentrant 80 % du combustible résineux le plus inflammable.
* **M (Mesurable) :** Atteindre un **temps d'attaque initiale inférieur à 10 minutes sur 85 % des départs de feux** en zone rouge résineuse (communes où le taux de pin maritime de la BD Forêt V2 dépasse 60 %), contre une moyenne de 18 minutes constatée en 2022.  
  *Garde-fou obligatoire :* Maintenir un plafond de latence maximale de 20 minutes sur 100 % des communes périurbaines et viticoles du département pour éviter tout délaissement territorial.
* **A (Atteignable) :** Positionnement dynamique des patrouilles mobiles de surveillance à des carrefours forestiers stratégiques dès 11h00 du matin les jours à risque.
* **R (Réaliste) :** Respecte les effectifs de garde disponibles au SDIS 33 sans surcoût d'acquisition d'engins supplémentaires.
* **T (Temporel) :** Déploiement cartographique effectif dès le 15 juin 2027.

### Objectif SMART 3 : Dimensionnement horaire des astreintes et maîtrise budgétaire (Question Q6)

* **S (Spécifique) :** Réaligner les plannings de garde postée des sapeurs-pompiers professionnels et volontaires sur le créneau horaire d'aléa thermique maximal.
* **M (Mesurable) :** Sécuriser un **taux de disponibilité opérationnelle immédiate supérieur à 90 %** (engins prêts à partir en moins de 3 minutes) sur la plage horaire critique 14h00-18h00 UTC lors des journées classées Orange ou Rouge.  
  *Garde-fou budgétaire :* Plafonner les heures supplémentaires hors de ce créneau critique sous 15 % du volume total des astreintes estivales, en se basant sur le coût moyen forfaitaire d'une vacation de garde postée (~120 à 150 € par équipier pour 8h).
* **A (Atteignable) :** Décalage des vacations classiques 8h00-16h00 vers des vacations modulées 12h00-20h00 lors des journées d'alerte.
* **R (Réaliste) :** Compatible avec les accords locaux d'aménagement du temps de travail du SDIS 33 et les conventions employeurs des pompiers volontaires.
* **T (Temporel) :** Évaluation hebdomadaire continue sur les mois de juillet et août 2027.

---

## 3. Matrice d'utilité et de test des hypothèses (Conforme Slide 5 du Cours 4)

Chaque hypothèse sous-jacente à nos objectifs SMART est formellement auditée selon les 3 filtres d'utilité exigés par Marine Prost :
1. *Si l'hypothèse est vraie / fausse, que fait le SDIS différemment ?*
2. *La variable est-elle connue avant la décision (Causalité temporelle ex-ante stricte) ?*
3. *Apporte-t-elle quelque chose que l'indice Météo des forêts seul ne dit pas déjà ?*

| Question analytique | Hypothèse testée | 1. Décision si Vraie vs si Fausse | 2. Causalité temporelle ex-ante (Connue avant ?) | 3. Apport par rapport à l'indice Météo seul |
| :--- | :--- | :--- | :--- | :--- |
| **Q1 (Massifs prioritaires)** | 80 % des surfaces détruites se concentrent sur moins de 20 % des communes à fort taux de résineux (> 60 %). | **Si vraie :** Prépositionner les engins lourds au cœur des massifs sud.<br>**Si fausse :** Répartir uniformément les camions sur tout le département. | **Oui :** Le taux de résineux (BD Forêt V2) est statique et connu avant la saison. | L'indice Météo-France ignore l'essence des arbres ; la BD Forêt apporte la masse réelle de combustible au sol. |
| **Q2 (Fiabilité vigilance)** | L'indice départemental sous-estime le danger lors des journées à vent sec localisé (rafales > 30 km/h et $U < 30\%$). | **Si vraie :** Abaisser le seuil d'alerte dès que le vent dépasse 30 km/h.<br>**Si fausse :** Conserver les seuils nationaux sans modification. | **Oui :** Les prévisions de vent et d'humidité à J+1 et J+2 sont disponibles dès 17h00 la veille. | L'indice départemental moyenne les valeurs ; les stations terrestres isolent les couloirs de vent locaux. |
| **Q4 (Départs sous vigilance basse)** | Les feux survenus sous indice Vert/Jaune résultent de micro-climats chauds non captés par la maille départementale. | **Si vraie :** Déclencher des patrouilles légères locales sur alertes de stations.<br>**Si fausse :** Revoir l'origine humaine des éclosions (malveillance, mégots). | **Oui :** Les mesures des 31 stations terrestres sont relevées en temps réel heure par heure. | Corrige l'effet de lissage spatial de l'indice national Météo des forêts. |
| **Q5 (Gravité et surface)** | Une attaque initiale sous 10 minutes maintient 85 % des feux sous le seuil critique de 1 hectare. | **Si vraie :** Privilégier les patrouilles roulantes en forêt plutôt que l'attente en caserne.<br>**Si fausse :** Maintenir les équipages au centre de secours. | **Oui :** La localisation des pistes DFCI et des points d'eau est cartographiée en amont. | La BDIFF permet de corréler le délai d'intervention initial avec la surface finale détruite. |
| **Q6 (Ventilation horaire)** | Plus de 80 % des départs majeurs éclatent entre 14h00 et 18h00 UTC sous l'effet du dôme thermique. | **Si vraie :** Décaler les vacations d'astreinte sur la tranche 12h00-20h00.<br>**Si fausse :** Conserver les gardes postées de jour de 8h00 à 16h00. | **Oui :** L'heure de l'astreinte est planifiée la veille pour le lendemain. | Optimise l'utilisation des deniers publics et des vacations sans surcoût budgétaire. |

---

## 4. Règles méthodologiques de robustesse et gestion des cas limites (Records 22 et 26)

* **Règle d'attribution des feux multi-jours :**  
  Un incendie majeur s'étendant sur plusieurs jours ou semaines (tel que le feu de Landiras) est **rattaché exclusivement à sa date et son heure de première alerte** (`date_premiere_alerte` dans la BDIFF). La décision de dimensionnement des secours se prend au matin du jour d'éclosion, les jours suivants relevant de la conduite de crise et de la lutte lourde.
* **Périmètre temporel estival strict :**  
  Les indicateurs sont calculés sur la période estivale active (1er juin au 30 septembre), correspondant à la publication effective de la Météo des forêts. Les feux hivernaux de débroussaillement sont formellement isolés pour ne pas introduire de myopie temporelle.
* **Filtrage des valeurs aberrantes et seuil plancher :**  
  Pour éviter que des départs de feu insignifiants (mégots étouffés, feux de poubelle de 0,001 ha) ne faussent le taux de feux non anticipés, un seuil plancher de gravité opérationnelle à **5 hectares** est appliqué au numérateur comme au dénominateur.
