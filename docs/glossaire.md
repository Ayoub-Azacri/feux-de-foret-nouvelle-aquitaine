# Glossaire : Nouvelle-Aquitaine (Gironde - SDIS 33)

Dernière mise à jour : 2026-11-17

## Chef de centre

* **Définition :** Officier de sapeurs-pompiers responsable du commandement opérationnel, de la gestion des effectifs et du casernement d'un centre d'incendie et de secours (CIS) sur un secteur territorial donné.
* **Registre :** Statut et titre hiérarchique opérationnel (officier de sapeurs-pompiers).
* **Contexte d'usage :** Commandement d'un Centre d'Incendie et de Secours (CIS), arbitrage local de l'engagement des gardes et concertation avec la direction du SDIS.
* **Synonymes et antonymes :** Synonyme : Commandant de caserne, chef de CIS. Antonyme : Opérateur de salle opérationnelle, pompier en mission d'exécution.
* **Sources et colonnes :** E-mail de cadrage SDIS 33 (« Certains chefs de centre estiment... »), organigramme territorial officiel du SDIS 33.
* **Divergences :** Pour la direction, les chefs de centre doivent appliquer une consigne départementale unique. Sur le terrain, chaque chef de centre module son appréciation selon la sensibilité de son massif local (massif dunaire littoral, forêt de pins des Landes de Gascogne ou vignoble).
* **Règle retenue :** Considéré comme une entité de décision territoriale locale, rattachée aux groupements de secours du SDIS 33.
* **Unité ou granularité :** Une caserne ou un centre d'incendie et de secours (CIS).
* **Exemple :** Chef de centre du CIS de Belin-Béliet ou du CIS de La Teste-de-Buch.
* **Statut :** validé.
* **Origine de la définition :** Règlement opérationnel du SDIS 33 et Code général des collectivités territoriales.
* **Ajouté par :** Youssef EL HAJJI et Youssef DEKHAIL, 2026-11-16.

## Danger élevé

* **Définition :** Niveau d'alerte météorologique signalant des conditions particulièrement favorables aux éclosions rapides et aux propagations violentes de feux de végétation (sécheresse de la litière, température élevée, vent soutenu).
* **Registre :** Échelon de vigilance météorologique et opérationnelle.
* **Contexte d'usage :** Qualification du risque d'incendie diffusée par Météo-France et prise de décision de renforts par le CODIS 33.
* **Synonymes et antonymes :** Synonyme : Vigilance Orange (niveau 3), risque feu sévère. Antonymes : Risque faible, vigilance Verte, situation calme.
* **Sources et colonnes :** E-mail SDIS 33, Météo des forêts (colonne niveau_j1 = 3 ou niveau_j2 = 3, correspondant à la couleur Orange).
* **Divergences :** Pour Météo-France, « élevé » équivaut strictement au niveau Orange (3). Pour certains chefs de centre, le terme englobe à la fois le niveau Orange (3) et le niveau Très élevé / Rouge (4). Pour les pompiers, le danger dépend aussi de la présence humaine et du vent local non mesuré par l'indice départemental.
* **Règle retenue :** Définir formellement le danger élevé comme le niveau Orange (valeur 3 dans niveau_j1), distinct du danger très élevé (Rouge, valeur 4).
* **Unité ou granularité :** Un jour par département.
* **Exemple :** Indice Orange (niveau 3) prévu pour la Gironde le 12 juillet 2022.
* **Statut :** validé.
* **Origine de la définition :** Météo-France (charte technique de la Météo des forêts) et SDIS 33.
* **Ajouté par :** Ayoub AZACRI et Omar HAKIK, 2026-11-16.

## Départ de feu

* **Définition :** Éclosion initiale d'une combustion libre et non maîtrisée en milieu naturel ou boisé, ayant nécessité l'engagement de moyens de secours ou ayant fait l'objet d'un signalement officiel.
* **Registre :** Événement opérationnel et qualification initiale de sinistre.
* **Contexte d'usage :** Déclaration d'alerte au CTA-CODIS et instruction statistique post-événement dans la BDIFF.
* **Synonymes et antonymes :** Synonymes : Éclosion, foyer naissant, incendie de forêt. Antonymes : Fausse alerte, feu maîtrisé, écobuage autorisé / feu prescrit.
* **Sources et colonnes :** E-mail SDIS 33 (« lutter au mieux contre les départs de feu »), BDIFF (colonne id_incendie, table des faits centraux), main courante opérationnelle CTA-CODIS.
* **Divergences :** Pour le centre de traitement de l'alerte (CTA-CODIS), un départ de feu correspond à tout appel pour fumée ou feu naissant, y compris fausses alertes ou feux éteints avant l'arrivée des secours. Pour la BDIFF, un départ de feu n'est comptabilisé que s'il a été instruit avec un rapport de constatation officiel et une surface brûlée mesurée.
* **Règle retenue :** Tout événement d'incendie enregistré avec un numéro unique officiel dans la BDIFF (id_incendie), ayant détruit au moins 1 mètre carré de végétation (surface > 0 ha).
* **Unité ou granularité :** Un événement d'incendie unique, géolocalisé et horodaté.
* **Exemple :** Incendie n° 2022-11533 déclaré le 12/07/2022 sur la commune de Landiras.
* **Statut :** validé.
* **Origine de la définition :** Ministère de l'Intérieur et BDIFF (circulaire interministérielle feux de forêt).
* **Ajouté par :** Ayoub AZACRI, Omar HAKIK et Youssef EL HAJJI, 2026-11-16.

## Département

* **Définition :** Circonscription administrative territoriale de la République française servant de périmètre d'action au Service Départemental d'Incendie et de Secours et de maille de diffusion de la Météo des forêts.
* **Registre :** Circonscription territoriale administrative et échelon d'organisation des services de secours.
* **Contexte d'usage :** Agrégation statistique des bilans de feux, vote du budget des secours et maille de diffusion de la Météo des forêts.
* **Synonymes et antonymes :** Synonyme : Circonscription départementale (code 33). Antonymes : Zone de défense zonale, région administrative, commune.
* **Sources et colonnes :** E-mail SDIS 33 (« sur tout le département »), Météo des forêts (colonnes num_dep et nom_dep), BDIFF (colonne code_departement), Admin Express Insee.
* **Divergences :** Pour l'Insee, le département 33 correspond à une limite administrative stricte de 535 communes. Pour les opérations des pompiers, le département intègre des accords d'entraide interdépartementale immédiate (pacte feux de forêt avec les SDIS 40 des Landes et SDIS 47 de Lot-et-Garonne sur le massif partagé des Landes de Gascogne) qui dépassent les frontières préfectorales.
* **Règle retenue :** Maille géographique administrative Insee à deux chiffres (33 pour la Gironde) pour les jointures entre tables, tout en isolant les zones de lisière interdépartementale.
* **Unité ou granularité :** Département administratif (code Insee sur 2 caractères).
* **Exemple :** Code département 33 (Gironde).
* **Statut :** validé.
* **Origine de la définition :** Code officiel géographique (Insee).
* **Ajouté par :** Youssef EL HAJJI et Omar HAKIK, 2026-11-16.

## Dispositif renforcé

* **Définition :** Posture opérationnelle préventive exceptionnelle ordonnée par la direction des secours, consistant à mobiliser des effectifs supplémentaires en caserne, à prépositionner des véhicules d'attaque en forêt et à armer les vigies lors des journées à fort risque d'incendie.
* **Registre :** Mesure opérationnelle et protocole d'astreinte préventive.
* **Contexte d'usage :** Mobilisation exceptionnelle de moyens humains et matériels en amont des éclosions sur ordre du commandement du SDIS 33.
* **Synonymes et antonymes :** Synonymes : Garde postée, mobilisation préventive, posture feux sévères. Antonymes : Posture de base, veille ordinaire, régime normal de caserne.
* **Sources et colonnes :** E-mail SDIS 33 (« déclencher le dispositif renforcé (patrouilles, guet, etc.) »), ordres de mobilisation opérationnelle CODIS.
* **Divergences :** Pour la direction financière, le dispositif renforcé représente un surcoût budgétaire direct (heures supplémentaires, usure du matériel, carburant). Pour les chefs de centre, c'est l'assurance d'un délai d'attaque initial inférieur à 10 minutes pour écraser tout départ de feu avant qu'il ne devienne incontrôlable.
* **Règle retenue :** Indicateur binaire journalier (activé ou non activé) associé au seuil d'alerte, dont l'impact budgétaire et opérationnel doit être calibré pour limiter les fausses alertes.
* **Unité ou granularité :** Une journée par massif ou département.
* **Exemple :** Mobilisation de 4 groupes d'intervention feux de forêt (GIFF) en garde postée à Hostens et Belin-Béliet.
* **Statut :** validé.
* **Origine de la définition :** Règlement opérationnel et doctrine zonale feux de forêt de Nouvelle-Aquitaine.
* **Ajouté par :** Ayoub AZACRI, Omar HAKIK et Youssef EL HAJJI, 2026-11-16.

## Guet armé / vigie

* **Définition :** Mesure active de surveillance territoriale combinant des observateurs postés dans des tours de guet surplombant le massif et des camions citernes feux de forêt (CCF) en patrouille mobile sur les pistes forestières, prêts à intervenir instantanément dès détection d'une fumée.
* **Registre :** Tactique de surveillance territoriale et de primo-intervention en milieu forestier.
* **Contexte d'usage :** Surveillance active depuis les points hauts DFCI et patrouilles mobiles de camions citernes sur pistes DFCI pendant les heures chaudes.
* **Synonymes et antonymes :** Synonymes : Vigie DFCI, patrouille armée, surveillance postée. Antonyme : Intervention sur appel téléphonique passif.
* **Sources et colonnes :** E-mail SDIS 33 (« patrouilles, guet, etc. »), réseau des tours de surveillance DFCI Gironde.
* **Divergences :** Pour le grand public, une vigie est une simple tour d'observation passive. Pour les sapeurs-pompiers, le guet est armé, ce qui signifie que l'équipe dispose d'une réserve d'eau et de matériel d'attaque immédiate dans le véhicule de patrouille.
* **Règle retenue :** Modalité opérationnelle constitutive du dispositif renforcé, mobilisée sur créneaux d'alerte diurnes (généralement de 12h00 à 20h00 en période estivale).
* **Unité ou granularité :** Unité de surveillance postée ou itinérante.
* **Exemple :** Vigie du Porge ou patrouille mobile sur le carroyage DFCI du Sud-Médoc.
* **Statut :** validé.
* **Origine de la définition :** Association DFCI Aquitaine et SDIS 33.
* **Ajouté par :** Omar HAKIK, 2026-11-16.

## Indice au plus bas

* **Définition :** Niveau d'évaluation météorologique indiquant une probabilité très faible d'incendie (végétation humide, températures fraîches, absence de vent fort).
* **Registre :** Qualification qualitative d'un niveau de risque météorologique minimal.
* **Contexte d'usage :** Évaluation rétrospective des départs de feux survenus hors conditions d'alerte officielle de Météo-France.
* **Synonymes et antonymes :** Synonyme : Niveau 1 (Vert / faible), risque résiduel. Antonymes : Pic de chaleur, alerte rouge, conditions d'embrasement généralisé.
* **Sources et colonnes :** E-mail SDIS 33 (« des feux partis des jours où l'indice était au plus bas »), Météo des forêts (colonnes niveau_j1 = 1 ou 2, couleur Verte ou Jaune).
* **Divergences :** La direction fait référence aux feux survenus sous indice faible. Pour Météo-France, l'indice 1 (Vert) n'indique jamais un risque zéro, mais signifie que les feux naissants s'éteignent facilement sans intervention massive. Pour les pompiers, un vent local fort ou une négligence humaine peut propager un feu même avec un indice vert.
* **Règle retenue :** Équivaut aux niveaux 1 (Vert / faible) et 2 (Jaune / modéré) de la Météo des forêts dans les requêtes de croisement avec la BDIFF.
* **Unité ou granularité :** Un jour par département.
* **Exemple :** Indice Vert (niveau 1) enregistré le 5 juin 2024 en Gironde.
* **Statut :** validé.
* **Origine de la définition :** Météo-France et analyse SDIS 33.
* **Ajouté par :** Youssef EL HAJJI et Omar HAKIK, 2026-11-16.

## Interface forêt-habitat

* **Définition :** Zone de transition géographique où les constructions humaines, habitations, lotissements et campings jouxtent ou s'entremêlent avec des formations végétales combustibles forestières.
* **Registre :** Concept géo-spatial et urbanistique d'exposition aux risques naturels (Wildland-Urban Interface).
* **Contexte d'usage :** Zonage prioritaire de défense des populations, application des Obligations Légales de Débroussaillement (OLD) et tactique de protection des points sensibles.
* **Synonymes et antonymes :** Synonymes : Lisière habitée, zone de contact forêt-bâti, interface périurbaine. Antonymes : Cœur de massif forestier isolé, zone urbaine dense continue sans végétation.
* **Sources et colonnes :** BD Forêt V2 de l'IGN (polygones formation_vegetale), BD TOPO Bâti, plans de prévention des risques (PPRIF).
* **Divergences :** Pour l'urbanisme, c'est une zone administrative soumise aux obligations légales de débroussaillement (OLD). Pour les pompiers, c'est la zone prioritaire où les vies humaines et les biens sont directement menacés, imposant de détourner des camions de la lisière forestière pour protéger les habitations.
* **Règle retenue :** Intersection spatiale entre un polygone forestier (notamment pin maritime) et une zone bâtie dans un rayon de 50 à 200 mètres.
* **Unité ou granularité :** Zone géographique ou polygone communal.
* **Exemple :** Quartiers résidentiels de La Teste-de-Buch en lisière de la forêt usagère lors des évacuations de juillet 2022.
* **Statut :** validé.
* **Origine de la définition :** Guide technique national PPRIF / Ministère de la Transition écologique.
* **Ajouté par :** Youssef DEKHAIL, 2026-11-16.

## Météo des forêts

* **Définition :** Système d'information et d'alerte météorologique quotidien publié par Météo-France de juin à septembre, quantifiant le niveau de danger d'incendie de végétation sur une échelle de 4 couleurs (vert, jaune, orange, rouge) à l'échelle départementale.
* **Registre :** Dispositif national d'information préventive et indice composite météorologique.
* **Contexte d'usage :** Communication grand public et indicateur d'aide à la décision pour le déclenchement des postures de vigilance feux de forêt.
* **Synonymes et antonymes :** Synonymes : Indice de danger feux de forêt, bulletin de vigilance incendie Météo-France. Antonymes : Météo des plages, bulletin météorologique synoptique général.
* **Sources et colonnes :** E-mail SDIS 33, Archives Météo des forêts (colonnes niveau_j1, niveau_j2, date, num_dep), modèle numérique AROME et calcul de l'Indice Forêt Météo (IFM).
* **Divergences :** Pour le public, c'est une consigne d'alerte générale. Pour le SDIS 33, c'est un indicateur externe critiqué parce qu'il n'intègre pas les spécificités de combustible locales (pin maritime face aux feuillus) et qu'il applique la même note pour tout le département.
* **Règle retenue :** Variable catégorielle ordonnée (1: Faible/Vert, 2: Modéré/Jaune, 3: Élevé/Orange, 4: Très élevé/Rouge) servant d'axe d'analyse pour évaluer les seuils.
* **Unité ou granularité :** Niveau journalier par département, diffusé pour J+1 et J+2.
* **Exemple :** Département de la Gironde (33) classé en niveau 3 (Orange) le 15 août 2024.
* **Statut :** validé.
* **Origine de la définition :** Météo-France (dossier technique officiel).
* **Ajouté par :** Ayoub AZACRI, Omar HAKIK, Youssef EL HAJJI et Youssef DEKHAIL, 2026-11-16.

## SDIS (SDIS 33)

* **Définition :** Service Départemental d'Incendie et de Secours de la Gironde, établissement public administratif territorialement compétent pour la prévention, la protection et la lutte contre les incendies et accidents sur le département 33.
* **Registre :** Acronyme institutionnel et établissement public administratif territorial.
* **Contexte d'usage :** Direction des opérations de secours, pilotage budgétaire et commandement départemental de la lutte contre les incendies.
* **Synonymes et antonymes :** Synonymes : Service Départemental d'Incendie et de Secours, corps départemental des sapeurs-pompiers. Antonymes : Service privé de sécurité, brigade militaire (BSPP / BMPM).
* **Sources et colonnes :** E-mail SDIS 33 (émetteur de la commande), Statistiques nationales des SDIS (DGSCGC / Ministère de l'Intérieur).
* **Divergences :** Pour le citoyen, les pompiers interviennent sans distinction budgétaire. Pour les gestionnaires publics, le SDIS dépend d'un budget autonome voté par le Conseil départemental et les communes, imposant une allocation financière stricte des moyens lors des campagnes feux.
* **Règle retenue :** Commanditaire officiel du projet décisionnel, dont les contraintes budgétaires et humaines orientent tous les arbitrages de modélisation.
* **Unité ou granularité :** Établissement public départemental.
* **Exemple :** SDIS 33 (Centre de commandement à Bordeaux, Groupements territoriaux Sud, Bassin, Médoc, Nord-Est).
* **Statut :** validé.
* **Origine de la définition :** Code général des collectivités territoriales (article L1424-1).
* **Ajouté par :** Ayoub AZACRI, Omar HAKIK, Youssef EL HAJJI et Youssef DEKHAIL, 2026-11-16.

## Seuil de déclenchement (seuil actuel)

* **Définition :** Règle ou valeur seuil de l'indice Météo des forêts à partir de laquelle la direction des opérations du SDIS 33 ordonne automatiquement l'activation des renforts préventifs (gardes postées, patrouilles de guet armé, conducteurs d'astreinte en caserne).
* **Registre :** Critère normatif et règle décisionnelle de gestion opérationnelle.
* **Contexte d'usage :** Arbitrage d'engagement financier et humain du SDIS 33 en fonction de l'indice journalier de danger.
* **Synonymes et antonymes :** Synonymes : Valeur charnière d'alerte, seuil de bascule, niveau de consigne. Antonymes : Déclenchement discrétionnaire, absence de protocole.
* **Sources et colonnes :** E-mail SDIS 33 (« Le seuil actuel ne nous convient pas »), consignes journalières opérationnelles CODIS.
* **Divergences :** Le débat interne porte sur le niveau précis de bascule : un seuil fixé trop bas (niveau Jaune ou Orange systématique) engendre une usure prématurée des effectifs et des dépenses excessives pour des journées sans départ de feu. Un seuil fixé trop haut (niveau Rouge strict) expose les secours à un retard critique lors des feux éclos sous conditions intermédiaires.
* **Règle retenue :** Seuil décisionnel paramétrable dans notre modèle (niveau 2, 3 ou 4), dont nous devons mesurer le ratio coût/efficacité et le taux de fausses alertes.
* **Unité ou granularité :** Niveau de vigilance (1 à 4) ou valeur d'indice IFM.
* **Exemple :** Déclenchement automatique des vigies dès que l'indice atteint le niveau 3 (Orange).
* **Statut :** à vérifier (doctrine exacte en vigueur à confirmer avec la direction du SDIS).
* **Origine de la définition :** Doctrine opérationnelle SDIS 33 et analyse de la commande.
* **Ajouté par :** Ayoub AZACRI et Youssef EL HAJJI, 2026-11-16.

## Surface brûlée

* **Définition :** Superficie totale de végétation forestière, naturelle ou agricole parcourue et détruite par les flammes lors d'un incendie, mesurée et validée par les autorités après extinction complète du sinistre.
* **Registre :** Grandeur quantitative et métrique d'impact écologique et économique.
* **Contexte d'usage :** Bilan officiel de fin d'intervention, cartographie des dégâts et instruction judiciaire dans la BDIFF.
* **Synonymes et antonymes :** Synonymes : Superficie parcourue par le feu, surface sinistrée, surface calcinée. Antonymes : Surface épargnée, zone refuge, massif préservé.
* **Sources et colonnes :** BDIFF (colonnes surface_foret, surface_autre_boisee, surface_non_boisee, exprimées en hectares).
* **Divergences :** Pour la presse, la surface brûlée est estimée à chaud à vue d'œil ou par satellite (conduisant parfois à des chiffres surévalués). Pour la BDIFF et les experts forestiers, la surface est arpentée avec précision au GPS sur le terrain après extinction complète.
* **Règle retenue :** Somme des surfaces forestières et boisées (surface_foret + surface_autre_boisee) mesurée en hectares, telle que certifiée dans la BDIFF.
* **Unité ou granularité :** Hectare (ha), avec précision au centième ou au dixième.
* **Exemple :** 20 800 hectares brûlés lors de l'incendie de Landiras en 2022.
* **Statut :** validé.
* **Origine de la définition :** BDIFF (norme nationale d'enregistrement des incendies de forêt).
* **Ajouté par :** Ayoub AZACRI, 2026-11-17.
