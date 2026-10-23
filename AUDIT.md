# Audit du prototype et contrôle final

23 octobre 2026 · Version 1.0

## Ancien fichier examiné

`index(20261023-132843).html` (655 lignes). Le prototype contenait Mifflin–St Jeor, une bascule Katch–McArdle, des pas estimés par cadence, ACSM tapis, MET musculation, TEF calculée et une calibration à deux pesées. Aucun stockage durable ni PWA.

Corrections : suppression de `variation de poids × 7 700 / jours` comme estimateur de maintenance ; suppression de la prévision hebdomadaire dérivée du même coefficient ; suppression de la « fourchette réaliste » ±5 %, des décalages fixes pour recomposition/sèche/surplus, de la masse maigre dite « exacte » et du « minimum hormonal » universel. La dépense tapis ACSM était plausible en domaine restreint mais son addition aux pas et aux autres composants rendait le modèle difficile à interpréter ; la V1 privilégie un facteur théorique unique, secondaire, et les observations réelles.

## Revue adversariale et corrections

- Correction de la relation palier J → alimentation J → pesée J+1, y compris graphiques et CSV.
- Validation rendue impossible avec seulement 14 jours récents après 35 jours écoulés ; deux blocs de 14 jours et complétude du palier exigés.
- Recommandations suspendues si la cible annoncée n’est pas réellement suivie ou si activité et qualité des apports changent.
- Distinction entre apport moyen observé et cible du dernier palier validé pour un retour éventuel.
- L’état visible n’est modifié qu’après transaction IndexedDB réussie ; sérialisation des écritures.
- Moyennes 7 jours masquées si moins de 5 valeurs ; entraînements cardio pris en compte.
- Fusion JSON : doublons identiques ignorés, conflits de journée/palier/profil refusés ; remplacement distinct avec confirmation. Restauration complète du profil et des préférences.

## Tests effectués

`npm test` : 21 tests réussis. Scénarios de stabilité, baisse, hausse récente, baisse des pas, jours manquants, macros incohérentes, saut isolé, hausse durable, correction rétroactive, round-trip du format JSON, doublons, dates civiles, palier non suivi, données insuffisantes sur 35 jours, cardio, moyennes incomplètes et fusion de profil. Vérification syntaxique Node des modules ; fichiers du service worker et du manifeste inspectés ; ressources statiques servies par un serveur HTTP local. Aucun jeu de démonstration dans la version utilisateur. Les essais IndexedDB et service worker utilisent des doubles de test Node : ils vérifient le code de sauvegarde et la logique de cache, sans simuler Safari.

## Limites connues

L’environnement de test ne disposait pas d’un navigateur Chromium installable ni d’un iPhone Safari accessible. **La persistance réelle après fermeture de Safari, l’installation à l’écran d’accueil, le fonctionnement hors ligne dans Safari et les téléchargements sur iOS restent à vérifier sur appareil réel avant un usage auquel on confie un historique unique.** Le navigateur peut évincer des données locales malgré une demande de stockage persistant ; exporter des sauvegardes JSON régulières. Un nouvel iPhone n’est pas synchronisé. La qualité de l’apport observé dépend de l’exhaustivité de Yazio ; aucun contrôle 4/4/9 ne repère un repas oublié. Le moteur ne détecte pas la composition corporelle ni ne garantit l’absence de gain de graisse. Les seuils statistiques ne constituent pas une validation clinique individuelle.
