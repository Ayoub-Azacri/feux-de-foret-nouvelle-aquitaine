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

*Gestion de la dérive temporelle, millésimes de la végétation et partitionnement des séries météo.*

---

## 9. Entrées attendues et qualité

<!-- Section 9 : Attribuée à Youssef EL HAJJI (Ticket #25 - Branche feature/spec-qualite-youssef-elhajji) -->

*Exigences par source, profilage réel de l'échantillon Gironde 2022 et 3 règles de test automatisées (quality gate).*

---

## 10. Architecture

<!-- Section 10 : Attribuée à Youssef DEKHAIL (Ticket #26 - Branche feature/spec-pipeline-youssef-dekhail) -->

*Tableau des 6 couches du pipeline et schéma d'architecture Mermaid dans docs/architecture.md.*

---

## 11. Contraintes

<!-- Section 11 : Attribuée à Youssef EL HAJJI (Ticket #25 - Branche feature/spec-qualite-youssef-elhajji) -->

*Respect des contraintes opérationnelles (outils gratuits, persistance brute, autonomie hors-ligne, données incomplètes).*

---

## 12. Planning de réalisation

<!-- Section 12 : Attribuée à Youssef DEKHAIL (Ticket #26 - Branche feature/spec-pipeline-youssef-dekhail) -->

*Jalons de livraison du pipeline et hypothèses techniques avant la soutenance.*

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
