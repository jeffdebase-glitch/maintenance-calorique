# Guide d’utilisation — Palier

## 1. Première ouverture

1. Ouvre [l’application Palier](https://jeffdebase-glitch.github.io/maintenance-calorique/).
2. Va dans **Réglages** puis **Profil**.
3. Renseigne les données nécessaires : sexe, âge, taille, poids et, si tu le connais, le taux de masse grasse.
4. Enregistre le profil.
5. L’application affiche une **estimation théorique** de départ. Elle sert uniquement de point de départ.
6. Choisis la cible calorique du premier palier. La cible est une hypothèse à tester, pas une maintenance certaine.

## 2. Installation sur iPhone

Dans Safari :

1. Ouvre l’URL de l’application.
2. Touche **Partager**.
3. Choisis **Ajouter à l’écran d’accueil**.
4. Ouvre ensuite l’icône **Palier**.

Commence la saisie dans l’application installée et conserve-la dans le même contexte. Safari et l’icône installée peuvent utiliser des stockages distincts.

## 3. Saisie quotidienne

Chaque matin, ouvre **Saisie** et renseigne :

- **Poids de ce matin** : pesée du jour, dans les conditions habituelles ;
- **Calories d’hier** ;
- **Protéines, glucides et lipides d’hier** ;
- **Pas d’hier** ;
- **Activité d’hier** : repos, musculation, cardio/tapis ou musculation + cardio.

La phrase à retenir est : **poids de ce matin + alimentation et activité d’hier**.

La durée d’entraînement et les informations de contexte sont facultatives. Utilise-les seulement lorsque la journée était inhabituelle : repas très salé ou riche en glucides, alcool, voyage, maladie, sommeil très court ou séance exceptionnelle.

Si une donnée manque, laisse le champ vide plutôt que d’inventer une valeur. L’application continue de fonctionner, mais la confiance diminue.

## 4. Contrôle des calories et macros

Palier compare les calories saisies avec :

4 × protéines + 4 × glucides + 9 × lipides

Le résultat est un contrôle de cohérence :

- **Cohérent** : écart faible ;
- **Léger écart** : vérification utile ;
- **Écart important** : relire Yazio et les unités.

Un écart ne prouve pas que la saisie est fausse : arrondis, fibres, polyols et règles d’étiquetage peuvent expliquer une partie de la différence. Le moteur ne remplace pas automatiquement les calories saisies.

## 5. Lire l’écran Aujourd’hui

L’écran principal répond à trois questions :

- **Où j’en suis ?** : phase du protocole et palier actuel ;
- **Ma tendance est-elle stable ?** : poids brut, moyenne mobile 7 jours et tendance récente ;
- **Que faire maintenant ?** : recommandation déterministe du moteur.

Les niveaux de confiance sont qualitatifs :

- **Faible** : peu de données, activité variable ou valeurs manquantes ;
- **Moyen** : données utilisables, mais période encore courte ou perturbée ;
- **Élevé** : plusieurs semaines cohérentes, données complètes et activité comparable.

Une pesée isolée ne déclenche pas de changement calorique. Une hausse rapide après une augmentation des glucides peut être compatible avec le glycogène, l’eau, le sodium ou le contenu digestif.

## 6. Comprendre les phases

L’application progresse de façon prudente :

- **Collecte** : trop peu de données pour conclure ;
- **Première observation** : la moyenne 7 jours devient visible ;
- **Analyse** : poids, calories, pas, activité et qualité des données sont comparés ;
- **Palier en observation** : après une modification, on attend avant de décider ;
- **Maintenance candidate** : l’apport semble compatible avec une stabilité dans les conditions observées ;
- **Maintenance validée** : l’observation est suffisamment longue et cohérente ;
- **Plus haut apport stable testé** : plus haut palier effectivement testé sans dérive durable compatible avec une prise de masse grasse, à activité comparable.

Le moteur peut proposer une hausse modeste, généralement de l’ordre de **+100 à +150 kcal/jour**. Il s’agit d’une règle opérationnelle : la proposition doit être confirmée par l’utilisateur et n’est jamais appliquée automatiquement.

## 7. Tendances et graphiques

Dans **Tendances** :

- **14 jours** : vérifier la réaction récente ;
- **30 jours** : suivre un palier ;
- **90 jours** : voir la tendance de fond ;
- **Tout** : consulter l’historique complet.

Le poids brut montre le bruit quotidien. La moyenne mobile 7 jours est la courbe principale pour juger la tendance. Les pas et l’activité servent à éviter d’attribuer trop vite une variation du poids aux calories lorsqu’une dépense a changé.

## 8. Quand suivre ou ne pas suivre une recommandation

Suis le palier actuel lorsque l’application indique de maintenir ou d’observer encore.

Ne réduis pas les calories sur la seule base :

- d’une pesée isolée ;
- de deux ou trois jours atypiques ;
- d’une hausse suivant une augmentation des glucides ;
- d’une journée très salée ;
- d’une séance inhabituelle.

Attends une tendance persistante, une activité comparable et des données suffisamment complètes. Si les pas baissent fortement, l’application réduit la confiance : il faut d’abord observer davantage.

## 9. Historique

Dans **Historique** :

- recherche une date ;
- ouvre une journée pour la modifier ;
- corrige une erreur ;
- supprime une entrée après confirmation.

Une seule entrée doit exister par date. Une correction rétroactive recalcule les indicateurs et les décisions concernés.

## 10. Sauvegarde et restauration

Dans **Réglages → Données** :

- **Export JSON** : sauvegarde complète de l’application, à utiliser régulièrement ;
- **Import JSON** : restauration après validation du format ;
- **Export CSV** : ouverture de l’historique dans Numbers, Excel ou Google Sheets.

Lors d’un import, choisis explicitement la fusion ou le remplacement si l’option est proposée. Vérifie la date du fichier avant de confirmer. Garde plusieurs sauvegardes datées, par exemple :

maintenance-backup-2026-10-23.json

Les données restent sur l’appareil. Elles ne sont pas envoyées automatiquement à GitHub ni à un autre serveur.

## 11. Hors ligne et mise à jour

Après une première ouverture avec Internet, l’application peut fonctionner hors connexion grâce au service worker. Les données restent dans IndexedDB.

Pour une mise à jour :

1. ouvre une fois l’application avec Internet ;
2. attends le chargement complet ;
3. vérifie que l’historique est présent ;
4. exporte un JSON avant toute opération importante.

Une mise à jour du code ne doit pas supprimer l’historique. En cas de doute, restaure la dernière sauvegarde JSON.

## 12. Configuration conseillée

Pour obtenir une calibration exploitable :

- pèse-toi le matin dans des conditions proches ;
- enregistre les calories de la veille aussi régulièrement que possible ;
- conserve une activité et un nombre de pas comparables pendant un palier ;
- évite de modifier simultanément calories, entraînement et pas ;
- note les journées atypiques au lieu de les supprimer ;
- exporte les données au moins une fois par semaine.

L’application estime une maintenance **dans les conditions observées**. Elle ne mesure pas un métabolisme immuable et ne diagnostique pas une adaptation métabolique ou une maladie.

## 13. Limites et santé

Palier est un outil de suivi expérimental, pas un dispositif médical. Les tendances ne permettent pas de diagnostiquer un trouble hormonal, une faible disponibilité énergétique ou une cause médicale.

En présence de symptômes importants ou persistants, demande un avis à un professionnel de santé.
