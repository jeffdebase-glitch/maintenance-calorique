# Méthodologie et règles du moteur

Version 1.0 · 23 octobre 2026. Palier aide à observer un apport **déclaré** associé à une stabilité pondérale ; il ne mesure pas la dépense énergétique et ne pose pas de diagnostic.

## Modèle temporel

Une entrée datée `J` contient le poids du matin `J` et les calories, macros, pas et activité de `J−1`. Un palier daté `J` concerne l’alimentation du jour `J`, donc sa première pesée associée peut être celle du matin `J+1`. Le moteur n’utilise jamais la pesée de `J` pour juger le nouveau palier.

## Estimation initiale

Mifflin–St Jeor : homme `10p + 6,25t − 5a + 5`, femme `10p + 6,25t − 5a − 161`, avec p en kg, t en cm et a en années. Si un taux de masse grasse est renseigné : Katch–McArdle `370 + 21,6 × masse maigre estimée`. Un facteur global de 1,30 / 1,45 / 1,60 illustre un ordre de grandeur d’entretien ; ce n’est pas une mesure personnalisée. Pas d’addition séparée des pas, du tapis, de la musculation ou de la thermogenèse alimentaire : ces composantes sont déjà représentées de façon approximative par le facteur. Les observations ne sont jamais remplacées par un nouveau résultat d’équation.

## Statistique et décision

- La moyenne mobile du graphique requiert au moins 5 pesées sur les 7 jours civils précédents ; sinon elle reste vide.
- La tendance sur 14 jours associe la différence entre deux moyennes de 7 jours **non chevauchantes** et la pente médiane de paires de Theil–Sen (paires séparées de 3 jours ou plus). Elle est « stabilité probable » si les deux indicateurs restent dans ±0,20 % du poids par semaine ; « hausse » ou « baisse » si les deux dépassent la bande dans le même sens ; sinon « incertain ». La bande est un seuil pratique conservateur, pas une propriété biologique universelle. La moyenne des deux chiffres est une indication descriptive, jamais une prévision de graisse.
- Chaque fenêtre de 14 jours après acclimatation demande au moins 10 pesées, 10 apports et 10 nombres de pas. La comparaison des deux semaines de pas exige 5 valeurs dans chacune. Variation d’activité : à la fois ≥20 % et ≥1 500 pas/j en moyenne, ou ≥3 entraînements de différence entre les semaines. Ces valeurs sont des règles opérationnelles.
- Le palier est réellement testé si l’apport déclaré moyen des 14 derniers jours reste à ±max(150 kcal, 7,5 %) de la cible. Une évolution importante de l’apport entre début et fin du palier empêche sa qualification de stabilité. Un journal alimentaire peut rester incomplet même si ses macros sont cohérentes.
- Après un palier, les quatre premières pesées associées (matins J+1 à J+4) sont exclues de l’analyse. Avant le matin J+18 : pas de décision calorique. Dès 18 jours et avec données suffisantes, une baisse concordante à activité comparable peut proposer **+100 kcal/j**, confirmation manuelle obligatoire. Une hausse récente conduit d’abord à maintenir et observer.
- À 21 jours ou plus, un palier peut devenir candidat si les données depuis la fin de l’acclimatation sont au moins complètes à 75 %, si les 14 derniers jours montrent une stabilité et si l’activité et l’apport sont comparables. La maintenance observée affichée est l’apport déclaré moyen des 14 derniers jours arrondi aux 50 kcal.
- À 35 jours ou plus, une validation exige en outre deux périodes consécutives de 14 jours suffisamment renseignées et stables, avec activité et apport comparables. Le plus haut apport stable testé ne retient que ces paliers validés lorsque leur activité reste comparable à la période actuelle ; il reste indisponible si cette comparaison manque. En cas de deux périodes de hausse au-dessus d’un palier antérieurement validé, le moteur peut proposer de **revenir à la cible de ce palier**, jamais imposer le changement.
- La confiance « faible / moyen / élevé » est qualitative. « Élevé » exige un palier validé et au moins 12 pesées et 12 apports récents. Aucune probabilité chiffrée n’est calculée.

Une hausse après plus de glucides peut inclure eau, glycogène ou contenu digestif, mais le moteur ne peut pas identifier la composition de cette hausse chez une personne. Une stabilisation de la masse ne prouve pas non plus l’absence de changement de composition corporelle. Les seuils et durées sont modifiables dans `RULES` de `engine.js` : leur choix est prudent, non validé comme règle clinique universelle.

## Macros et données

Contrôle `4×protéines + 4×glucides + 9×lipides` : écart « léger » au-delà de max(75 kcal, 8 % des calories saisies), « important » au-delà de max(150 kcal, 15 %). Les fibres, polyols, arrondis et bases nutritionnelles expliquent une partie des écarts. Le moteur conserve toujours les calories déclarées et ne corrige jamais la valeur automatiquement. Les recommandations de protéines de l’ISSN pour la plupart des personnes actives se situent autour de 1,4–2,0 g/kg/j ; aucune cible de macros obligatoire ni « minimum hormonal » unique n’est imposé.

## Sources principales

- Hall KD et al. (2011), modèle dynamique de poids, *Lancet*. https://pubmed.ncbi.nlm.nih.gov/21872751/
- Hall KD & Chow CC (2013), limites de la règle 3 500 kcal/livre, *International Journal of Obesity*. https://pmc.ncbi.nlm.nih.gov/articles/PMC3859816/
- NIDDK, documentation du Body Weight Planner. https://www.niddk.nih.gov/research-funding/at-niddk/labs-branches/laboratory-biological-modeling/integrative-physiology-section/research/body-weight-planner
- Mifflin MD et al. (1990), équation de repos, *AJCN*. https://pubmed.ncbi.nlm.nih.gov/2305711/
- Variabilité quotidienne des pesées (2023 ; étude sur une personne, généralisation limitée). https://pubmed.ncbi.nlm.nih.gov/37955103/
- Fernández-Elías VE et al. (2015), glycogène et eau. https://pubmed.ncbi.nlm.nih.gov/25911631/
- Nunes CL et al. (2022), revue systématique de thermogenèse adaptative. https://pubmed.ncbi.nlm.nih.gov/33762040/
- Levine JA et al. (1999), variabilité du NEAT, *Science*. https://pubmed.ncbi.nlm.nih.gov/9880251/
- Jäger R et al. (2017), position ISSN sur protéines et sport. https://pubmed.ncbi.nlm.nih.gov/28642676/
- Burrows TL et al. (2020), limites des apports auto-déclarés. https://pubmed.ncbi.nlm.nih.gov/31920966/
- IOC (2023), consensus REDs : l’application ne peut pas diagnostiquer une faible disponibilité énergétique. https://bjsm.bmj.com/content/57/17/1073.abstract
