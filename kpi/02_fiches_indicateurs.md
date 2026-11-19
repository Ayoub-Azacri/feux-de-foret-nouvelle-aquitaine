# Jeu d'indicateurs v0, Audit RACER et Garde-fous opérationnels

* **Commanditaire :** Direction départementale du SDIS 33 (Gironde, Nouvelle-Aquitaine)
* **Cadre académique :** HETIC Master MD5 · Module UE01.B Définition des KPI et DataViz décisionnelle
* **Enseignante :** Marine PROST
* **Certification :** Titre RNCP 36209 Niveau 7 (Compétence CC2.1)
* **Auteur :** Youssef EL HAJJI (Responsable qualité et conformité)
* **Ticket associé :** Issue [#41](https://github.com/Ayoub-Azacri/feux-de-foret-nouvelle-aquitaine/issues/41)
* **Branche dédiée :** `feature/kpi-fiches-indicateurs`
* **Branche cible (PR) :** `dev`
* **Relecteur officiel :** Omar HAKIK (`@OmarHAKIK`, Responsable sources & cohérence)

---

## 1. Fiche du KPI Principal : Taux de feux non anticipés (Alerting & Vigilance)

| Champ de spécification | Description technique et opérationnelle |
| :--- | :--- |
| **Questions décisionnelles servies** | Question Q2 (Fiabilité du seuil Météo des forêts) et Question Q4 (Départs sous vigilance modérée). |
| **Objectif SMART associé** | Objectif SMART 1 (Plafonner à moins de 15 % les feux de plus de 5 ha survenus sous vigilance basse). |
| **Rôle dans le jeu d'indicateurs** | **KPI Principal** : Indice décisif qui conditionne la révision du seuil de mobilisation départementale. |
| **Numérateur** | Nombre d'incendies de forêt en Gironde avec surface brûlée finale $> 5$ ha survenus un jour où la vigilance prévue à J+1 (`niveau_j1`) est strictement inférieure au seuil critique $N$ ($N \in \{2, 3\}$). |
| **Dénominateur** | Nombre total d'incendies de forêt avec surface brûlée finale $> 5$ ha enregistrés sur le département 33 durant la période estivale active. |
| **Unité** | Pourcentage (%) |
| **Formule mathématique** | `(COUNT(feux[surface > 5ha AND niveau_j1 < N]) / COUNT(feux[surface > 5ha])) * 100` |
| **Paramètres ajustables** | Seuil critique $N$ : $N=2$ (Jaune) ou $N=3$ (Orange, valeur par défaut retenue). |
| **Périmètre et temporalité** | Grain spatial : communal Insee. Grain temporel : journalier. Période : 1er juin au 30 septembre. |
| **Sources et champs requis** | BDIFF (`surface_totale_brulee_ha`, `date_premiere_alerte`, `code_insee`) et Météo des forêts (`niveau_j1`, `num_dep = '33'`). |
| **Faisabilité et lignes utilisables** | 100 % de complétude sur les dates et surfaces de l'échantillon 2022. 122 jours estivaux complets sans valeurs manquantes dans les archives MDF. |
| **Proxy et limites documentées** | Les incendies multi-jours sont rattachés exclusivement à leur date de première alerte (`date_premiere_alerte`). Les éclosions nocturnes accidentelles d'origine humaine non liées à l'aléa météorologique constituent un biais documenté. |
| **Décision opérationnelle permise** | Si le taux dépasse 15 % : abaissement du seuil critique $N$ et déclenchement précoce du dispositif renforcé. Si le taux est faible : contrôle immédiat du garde-fou pour éviter la sur-mobilisation inutile. |

---

## 2. Garde-fou obligatoire du KPI Principal : Taux de fausses alertes

Conformément à la loi de Goodhart, pour contrer la tentation d'abaisser artificiellement le seuil $N$ au niveau Vert pour obtenir un taux de 0 % de feux non anticipés, ce contrepoids est obligatoirement surveillé :

| Champ de spécification | Description technique et opérationnelle |
| :--- | :--- |
| **Rôle dans le jeu** | **Garde-fou obligatoire (Indicateur contrepoids opposé au KPI 1)**. |
| **Numérateur** | Nombre de journées estivales en Gironde où la vigilance Météo des forêts est $\ge N$ mais où aucun départ de feu $> 1$ ha n'a été constaté. |
| **Dénominateur** | Nombre total de journées estivales où la vigilance Météo des forêts était $\ge N$. |
| **Unité** | Pourcentage (%) |
| **Formule mathématique** | `(COUNT(jours[niveau_j1 >= N AND feux_sup_1ha == 0]) / COUNT(jours[niveau_j1 >= N])) * 100` |
| **Plafond acceptable** | **Maximum 35 % de fausses alertes tolérées**. Au-delà de ce seuil, les équipages de pompiers volontaires sont démobilisés et le budget d'astreinte est gaspillé. |
| **Risque résiduel identifié** | Une journée d'alerte élevée sans feu n'est pas nécessairement une fausse alerte technique : les patrouilles préventives sur le terrain ont pu dissuader les comportements imprudents ou étouffer des départs naissants à 0,01 ha. |

---

## 3. Fiches des KPI Secondaires : Déploiement spatial et Astreintes

### KPI Secondaire 1 : Taux d'attaque initiale rapide en zone critique (Massifs de pin)

| Champ de spécification | Description technique et opérationnelle |
| :--- | :--- |
| **Questions décisionnelles servies** | Question Q1 (Massifs prioritaires) et Question Q5 (Délai d'intervention initial). |
| **Objectif SMART associé** | Objectif SMART 2 (Attaque en moins de 10 min sur 85 % des départs en zone résineuse). |
| **Rôle dans le jeu** | **KPI Secondaire (Déploiement spatial)** : Mesure l'efficacité du prépositionnement des engins (CCF). |
| **Formule mathématique** | `(COUNT(feux_zone_resineuse[delai_attaque <= 10 min]) / COUNT(feux_zone_resineuse)) * 100` |
| **Sources et champs requis** | BDIFF (`heure_alerte`, `heure_premiere_intervention`, `code_insee`) croisée avec la BD Forêt V2 (taux communal de pin maritime $> 60\%$). |
| **Garde-fou associé** | **Plafond de latence hors massif** : Le temps d'intervention sur les communes viticoles et périurbaines ne doit jamais dépasser 20 minutes (interdiction de délaisser le reste du territoire). |

### KPI Secondaire 2 : Taux de disponibilité opérationnelle en pic thermique (14h-18h UTC)

| Champ de spécification | Description technique et opérationnelle |
| :--- | :--- |
| **Question décisionnelle servie** | Question Q6 (Dimensionnement horaire des astreintes et gardes postées). |
| **Objectif SMART associé** | Objectif SMART 3 (Garantir 90 % de disponibilité des équipages en moins de 3 min sur 14h-18h UTC). |
| **Rôle dans le jeu** | **KPI Secondaire (Ressources humaines)** : Valide le décalage des vacations de garde sur le pic thermique. |
| **Formule mathématique** | `(Heures d'engins armés prêts au départ en < 3 min sur 14h-18h / Heures d'astreinte totales 14h-18h) * 100` |
| **Garde-fou associé** | **Plafonnement des heures supplémentaires hors pic** sous 15 % du volume total, basé sur le coût forfaitaire moyen d'une vacation de 8h (~120 à 150 € par équipier). |

---

## 4. Grille d'évaluation RACER du jeu d'indicateurs

Chaque indicateur est audité selon la grille de la Commission européenne (noté de 1 à 5 sur 5 dimensions) :

| Indicateur | Relevant | Accepted | Credible | Easy | Robust | Score global |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Taux de feux non anticipés (KPI Principal)** | **5/5 :** Répond directement à la révision des seuils demandée par le SDIS 33. | **4/5 :** Aligné sur la nomenclature Météo des forêts validée dans `docs/glossaire.md`. | **5/5 :** Compréhensible au premier coup d'œil par les officiers (Test Jean-Jacques). | **5/5 :** Calcul automatique en SQL sous DuckDB sans enquête terrain lourde. | **4/5 :** Seuil de 5 ha insensible au micro-bruit des petits départs déclaratifs. | **23/25 (Validé)** |
| **Taux de fausses alertes (Garde-fou)** | **5/5 :** Mesure l'efficience économique et la fatigue opérationnelle. | **5/5 :** Terme canonique défini et partagé dans le glossaire. | **4/5 :** Évite la dérive sécuritaire d'une métrique d'alerte isolée. | **5/5 :** Requête DuckDB directe sur les tables de fait vigilance. | **4/5 :** Filtre plancher à 1 ha pour stabiliser le dénominateur. | **23/25 (Validé)** |
| **Attaque rapide < 10 min en zone critique** | **5/5 :** Permet d'arbitrer les rondes de patrouille par massif. | **4/5 :** Basé sur le découpage officiel Insee et les massifs DFCI. | **5/5 :** Objectif de 10 minutes clair et partagé par la doctrine pompiers. | **4/5 :** Nécessite la jointure spatiale préalable avec la BD Forêt V2. | **5/5 :** Insensible aux fluctuations climatiques annuelles. | **23/25 (Validé)** |
| **Disponibilité pic 14h-18h UTC** | **4/5 :** Cible la plage horaire concentrant 80 % des feux estivaux. | **4/5 :** Conforme aux conventions de temps de travail des pompiers. | **4/5 :** Justifie l'aménagement des plannings de vacations de garde. | **4/5 :** Calculable sur les mains courantes d'astreinte. | **4/5 :** Plafonnement des heures sup limitant les dérives budgétaires. | **21/25 (Validé)** |

---

## 5. Analyse Pre-Mortem (3 scénarios d'échec anticipés à 1 an)

Nous projetons que, dans un an (septembre 2027), le SDIS 33 a pris une mauvaise décision en suivant aveuglément ces indicateurs.

| N° | Scénario d'échec plausible | Probabilité | Gravité | Garde-fou préventif associé |
| :--- | :--- | :--- | :--- | :--- |
| **1** | **Biais de sur-mobilisation permanente :** Pour faire chuter le taux de feux non anticipés, le commandement abaisse le seuil d'alerte à Jaune tout l'été. Résultat : épuisement des pompiers volontaires et dépassement de budget dès fin juillet. | Élevée | Majeure | Plafond strict sur le taux de fausses alertes (alerte immédiate si $> 35\%$) et affichage côte à côte des deux chiffres sur le dashboard. |
| **2** | **Délaissement des zones hors massif :** La concentration des patrouilles sur les communes à plus de 60 % de pin laisse le vignoble et les zones périurbaines sans surveillance lors d'un départ accidentel un jour de vent d'Est. | Moyenne | Critique | Plafond de latence maximale garanti (intervention en moins de 20 minutes sur 100 % des communes non patrouillées). |
| **3** | **Effet millésime et clés orphelines :** Une mise à jour du code commune Insee en 2026 modifie les centroïdes, créant des enregistrements orphelins et faussant le taux d'anticipation de 10 points. | Faible | Moyenne | Barrière de qualité Pytest bloquante d'intégrité référentielle sur la table de correspondance communale avant tout recalcul. |
