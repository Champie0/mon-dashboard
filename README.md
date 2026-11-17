# Mon dashboard

Dashboard personnel : tâches, habitudes, objectifs, finances et journal.

- **Site** : https://champie0.github.io/mon-dashboard/
- **Dépôt** : https://github.com/Champie0/mon-dashboard

## Ce que fait le dashboard

| Section | Contenu |
| --- | --- |
| Accueil | Date, salutation, phrase de motivation, 3 priorités du jour, habitudes à cocher, avancement de la journée, solde, échéances et rappels |
| Tâches | Titre, priorité, échéance, étiquettes, note. Filtres, tri, retards signalés |
| Habitudes | À cocher ou chiffrées (2 litres, 30 minutes…), grille des 30 derniers jours, séries, taux de réussite, courbe sur 12 semaines |
| Objectifs | Étapes à cocher, progression calculée, états (en cours, atteint, en pause, abandonné), échéances proches |
| Finances | Dépenses et revenus saisis à la main, plusieurs comptes, import de relevé CSV, catégories et règles, budgets, abonnements détectés |
| Journal | Humeur de 1 à 5, question du jour, notes, calendrier, recherche, courbe d'humeur |
| Rappels | Date, heure, répétition quotidienne ou hebdomadaire, notification du navigateur |
| Réglages | Mode sombre, verre dépoli, animations, ombres marquées, sauvegarde, listes de phrases et de questions, devise |

Tout tient dans un seul fichier, `index.html`, sans installation. Aucune connexion bancaire, aucun appel vers un service financier.

## Comment l'ouvrir

- **En ligne** : ouvrez https://champie0.github.io/mon-dashboard/ sur n'importe quel appareil.
- **Sans Internet** : téléchargez `index.html` et ouvrez-le dans un navigateur. Il fonctionne alors en mode local (la connexion GitHub demande l'adresse en ligne).

Sur téléphone, la navigation passe en bas de l'écran. Sur ordinateur, elle est dans la barre latérale. La touche `?` affiche les raccourcis clavier.

## Comment se connecter

1. Cliquez sur **Se connecter avec GitHub**, en haut à droite.
2. Acceptez la demande dans la fenêtre GitHub qui s'ouvre.
3. Votre nom et votre avatar s'affichent, avec le bouton **Se déconnecter**.

À la première connexion, si le navigateur contient déjà des données saisies en mode local, le dashboard propose une seule fois de les transférer vers votre compte.

La connexion demande un projet Firebase, à régler une seule fois : voir [Réglages à faire une fois](#réglages-à-faire-une-fois-firebase-et-github). Tant que ce n'est pas fait, le bouton explique la marche à suivre et le dashboard reste en mode local.

## Comment sauvegarder et restaurer mes données

- **Exporter** : Réglages > Sauvegarde > **Exporter mes données**. Vous obtenez un fichier `mon-dashboard-AAAA-MM-JJ.json` avec tous les modules.
- **Restaurer** : Réglages > Sauvegarde > **Restaurer une sauvegarde**. Le fichier est vérifié avant toute modification, puis un résumé s'affiche et une confirmation est demandée avant de remplacer les données actuelles. Un fichier abîmé est refusé sans rien toucher. Si un seul module du fichier est illisible, il est laissé de côté et les autres sont restaurés.
- L'export et la restauration fonctionnent connecté ou non.
- Si aucun export n'a été fait depuis plus de 30 jours, un rappel discret s'affiche en haut de l'écran.

Gardez vos fichiers d'export hors du dépôt : ils contiennent vos données réelles. Le `.gitignore` les exclut par précaution.

## Comment fonctionne la synchronisation

- **Mode local (non connecté)** : les données sont dans le stockage du navigateur (`localStorage`), sur cet appareil uniquement.
- **Mode connecté** : chaque module est enregistré dans Cloud Firestore, sous `users/{identifiant Firebase}/modules/{module}`. Les autres appareils connectés au même compte reçoivent les changements en quelques secondes.
- **Hors ligne** : une copie de vos données de compte reste sur l'appareil. Vous pouvez continuer à travailler ; les modules modifiés sont marqués « en attente » et envoyés dès que le réseau revient, même si la page a été fermée entre-temps. L'indicateur en haut à droite affiche l'état : *Mode local*, *Synchronisé*, *Envoi en cours…*, *Hors ligne*.
- **Conflits** : si le même module est modifié sur deux appareils avant qu'ils se soient synchronisés, la dernière modification envoyée remplace l'autre, pour ce module seulement.
- **Déconnexion** : la copie locale du compte est effacée de l'appareil (sauf s'il reste des modifications non envoyées), et le dashboard revient aux données du mode local.

### Sécurité

Les clés de `FIREBASE_CONFIG` dans `index.html` sont publiques par nature : elles désignent le projet, elles ne donnent aucun droit. Ce qui protège les données, ce sont les règles du fichier [`firestore.rules`](firestore.rules) : chaque utilisateur ne peut lire et modifier que ses propres documents. Le dépôt ne contient aucun secret : le secret de l'application OAuth GitHub se colle uniquement dans la console Firebase.

## Réglages à faire une fois (Firebase et GitHub)

Comptez une dizaine de minutes. Les noms de menus sont ceux de la console en français.

### A. Créer le projet Firebase

1. Ouvrez https://console.firebase.google.com et cliquez sur **Créer un projet**. Nom : `mon-dashboard`. Google Analytics : inutile, vous pouvez le désactiver.
2. Dans la page du projet, cliquez sur l'icône **Web** (`</>`) pour ajouter une application. Surnom : `Mon dashboard`. Ne cochez pas Firebase Hosting. Validez.
3. Firebase affiche un bloc `firebaseConfig`. Gardez cette page ouverte : il servira à l'étape D.

### B. Créer la base Firestore et publier les règles

4. Menu **Créer > Firestore Database** > **Créer une base de données**. Emplacement : choisissez-en un proche de vous (par exemple `europe-west6`, Zurich). Démarrez en **mode production**.
5. Onglet **Règles** : remplacez tout le contenu par celui du fichier [`firestore.rules`](firestore.rules), puis cliquez sur **Publier**.

### C. Activer la connexion GitHub

6. Menu **Créer > Authentication** > **Commencer** > onglet **Mode de connexion** > **GitHub** > **Activer**. Firebase affiche une **URL de rappel d'autorisation** du type `https://VOTRE-PROJET.firebaseapp.com/__/auth/handler`. Copiez-la et laissez cette fenêtre ouverte.
7. Dans GitHub : photo de profil > **Settings** > **Developer settings** > **OAuth Apps** > **New OAuth App** (accès direct : https://github.com/settings/applications/new).
   - Application name : `Mon dashboard`
   - Homepage URL : `https://champie0.github.io/mon-dashboard/`
   - Authorization callback URL : l'URL copiée à l'étape 6
   - Cliquez sur **Register application**.
8. Sur la page de l'application GitHub : copiez le **Client ID**, puis cliquez sur **Generate a new client secret** et copiez le secret (il n'est affiché qu'une fois).
9. Revenez dans Firebase (fenêtre de l'étape 6) : collez l'**ID client** et le **code secret du client**, puis **Enregistrer**.
10. Toujours dans Authentication : onglet **Paramètres** > **Domaines autorisés** > **Ajouter un domaine** : `champie0.github.io`.

### D. Renseigner la configuration dans le dashboard

11. Dans `index.html`, cherchez `const FIREBASE_CONFIG` et remplacez les six valeurs vides par celles du bloc `firebaseConfig` de l'étape 3.
12. Enregistrez, faites un commit et poussez sur `main`. GitHub Pages se met à jour en une à deux minutes.

### E. Conseillé : limiter la clé au site

13. Dans https://console.cloud.google.com/apis/credentials (même projet), ouvrez la clé **Browser key**, choisissez **Sites Web** dans les restrictions et ajoutez `https://champie0.github.io/*` et `https://VOTRE-PROJET.firebaseapp.com/*`.

## Tests

La liste des vérifications à faire à la main, module par module, est dans [`TESTS.md`](TESTS.md).

## Hypothèses retenues

Faute d'indication, ces choix ont été faits. Ils sont tous modifiables.

- **Devise** : CHF par défaut. Elle se change dans Réglages > Finances (CHF, EUR, USD, CAD, GBP).
- **Semaine** : elle commence le lundi.
- **Projet Firebase** : il n'existe pas encore, donc `FIREBASE_CONFIG` est vide et le dashboard démarre en mode local.
- **Design** : même langage que GainsTracker. Mode clair « papier » par défaut et mode sombre « encre », neutres chauds avec terracotta et olive, verre dépoli réservé à la barre latérale et à la barre du haut, contenu sur des surfaces opaques.
- **Polices** : celles du système (SF Pro sur Apple, Segoe UI Variable sur Windows), donc rien à télécharger.
- **Fond** : dégradés chauds et léger grain générés en CSS, sans image externe.
- **Notifications** : elles s'affichent tant que le dashboard est ouvert dans un onglet. Sur certains téléphones, le navigateur les refuse ; les rappels apparaissent alors dans l'Accueil.
- **Réglages d'affichage** (mode sombre, verre dépoli, animations, ombres marquées) : mémorisés par appareil, pas par compte, puisqu'ils dépendent de la puissance de chaque machine.
- **Virements entre comptes** : à saisir comme une dépense sur un compte et un revenu sur l'autre.

## Organisation des données

Les données sont rangées par module (`home`, `tasks`, `habits`, `goals`, `finance`, `journal`, `reminders`). Chaque module porte un numéro de version (`v`) et passe par une fonction de vérification à chaque lecture (navigateur, compte ou fichier importé). Si un module est illisible, il est mis de côté (une copie reste téléchargeable), il repart à vide et les autres continuent de fonctionner. Pour faire évoluer un format : augmenter `SCHEMA` et compléter la fonction `migrate()` dans `index.html`.

## Fichiers du dépôt

| Fichier | Rôle |
| --- | --- |
| `index.html` | Le dashboard complet (interface, styles, code) |
| `firestore.rules` | Règles de sécurité à publier dans Firestore |
| `TESTS.md` | Checklist de tests manuels |
| `README.md` | Ce document |
| `.gitignore` | Fichiers à ne jamais publier |


## Assistant IA (planning)

La section **Assistant IA** (touche `8`) génère un planning à partir d'une demande en langage naturel (« je veux apprendre l'espagnol en 3 mois, 30 min par jour »). Le plan proposé (objectif et étapes, tâches datées, habitudes, rappels) s'affiche avec des cases à cocher et n'est ajouté au dashboard qu'après validation ; l'ajout est annulable.

- Tout se passe **en ligne** : aucun modèle local, la carte graphique n'est pas utilisée.
- Fournisseur : OpenRouter, avec un modèle gratuit (nom finissant par `:free`), sans carte bancaire. Les limites de débit de l'offre gratuite s'appliquent. Le modèle est modifiable.
- La clé API est enregistrée uniquement dans le navigateur (`md:ai`) : elle n'est ni synchronisée avec Firestore ni incluse dans l'export JSON.
- Par défaut, les titres des tâches en cours sont envoyés avec la demande pour éviter les conflits ; désactivable dans la configuration.

### Projets, historique et modèle utilisé

- **Projets** : chaque tâche peut appartenir à un projet (champ « Projet » du formulaire). Dans Tâches, le filtre « Projet » et l'affichage « Par projet » regroupent les tâches avec l'avancement de chaque projet. Les plans de l'assistant créent automatiquement un projet portant le nom du plan.
- **Historique** : les conversations avec l'assistant sont conservées (30 au plus) et se rouvrent depuis le bouton « Historique ». Elles restent sur l'appareil : ni synchronisées ni exportées.
- **Modèle utilisé** : sous chaque réponse, une ligne indique quel modèle gratuit a répondu.
