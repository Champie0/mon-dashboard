# Checklist de tests manuels

À faire sur le site en ligne, d'abord sans être connecté, puis connecté. Cochez au fur et à mesure.

## Démarrage et affichage

- [ ] Le site s'ouvre sans message d'erreur, en mode sombre, avec l'indicateur « Mode local ».
- [ ] Sur ordinateur, la barre latérale est visible. Sur téléphone, la navigation est en bas de l'écran et rien ne dépasse en largeur.
- [ ] Réglages > Mode clair : l'affichage change. Après rechargement de la page, le choix est conservé.
- [ ] Réglages > Animations désactivées : plus aucun mouvement. Le choix est conservé après rechargement.
- [ ] Réglages > Effets lumineux désactivés : les halos disparaissent. Le choix est conservé après rechargement.

## Accueil

- [ ] La date du jour est juste et la salutation correspond à l'heure (matin, après-midi, soir).
- [ ] « Autre phrase » change la phrase de motivation.
- [ ] « Choisir » permet de cocher 3 tâches au plus ; une quatrième est refusée avec un message.
- [ ] Cocher une priorité ou une habitude fait monter le pourcentage de la jauge.
- [ ] Le solde, les échéances proches et les rappels à venir s'affichent.

## Tâches

- [ ] Écrire un titre puis Entrée ajoute la tâche.
- [ ] « Ajouter avec détails » : priorité, échéance, étiquettes et note sont enregistrées.
- [ ] Modifier, terminer, rouvrir et supprimer fonctionnent. « Annuler » après une suppression rétablit la tâche.
- [ ] Une tâche dont l'échéance est passée porte la mention « En retard » et un liseré rose.
- [ ] Chaque filtre (statut, priorité, étiquette, période) et chaque tri (échéance, priorité) donne le résultat attendu.

## Habitudes

- [ ] Créer une habitude quotidienne à cocher, puis une habitude limitée à certains jours.
- [ ] Créer une habitude chiffrée (2 litres) : les boutons + et − changent la valeur, et elle est validée à 2.
- [ ] Dans la grille des 30 jours, cliquer sur un jour passé le coche ; recliquer le décoche. Les jours non prévus sont inactifs.
- [ ] La série en cours, la meilleure série et les taux changent en conséquence.
- [ ] Les courbes sur 12 semaines s'affichent.

## Objectifs

- [ ] Créer un objectif avec titre, description, échéance et catégorie.
- [ ] Ajouter trois étapes, en cocher une : la jauge affiche 33 %.
- [ ] Changer l'état (atteint, en pause, abandonné) puis filtrer par état.
- [ ] Un objectif en cours dont l'échéance est dans moins de 14 jours apparaît dans « Proches de l'échéance ».

## Finances

- [ ] Ajouter une dépense et un revenu : le solde et les dépenses du mois changent.
- [ ] Écrire « migros » dans le libellé d'une nouvelle dépense : la catégorie Alimentation est proposée.
- [ ] Ajouter un second compte avec un solde de départ : le total en tient compte.
- [ ] Importer un relevé CSV : l'aperçu s'affiche, les colonnes sont modifiables, rien n'est enregistré avant de valider.
- [ ] Importer le même fichier une seconde fois : toutes les lignes sont signalées comme doublons.
- [ ] Choisir un fichier qui n'est pas un CSV (une image, par exemple) : un message clair s'affiche, rien n'est modifié.
- [ ] Fixer un budget : à 80 % la mention « Proche de la limite » apparaît, au-delà « Budget dépassé ».
- [ ] Une dépense identique sur trois mois de suite apparaît dans « Abonnements détectés ».
- [ ] Modifier la liste des catégories et une règle, puis vérifier qu'elles s'appliquent.

## Journal

- [ ] Choisir une humeur, écrire une note : « Enregistré à … » s'affiche sans cliquer nulle part.
- [ ] « Autre question » change la question du jour.
- [ ] Le jour apparaît dans le calendrier avec l'icône de l'humeur ; cliquer sur un autre jour ouvre son entrée.
- [ ] La recherche retrouve un mot d'une note, avec ou sans accents.
- [ ] La courbe d'humeur montre les jours notés.

## Rappels

- [ ] Créer un rappel dans deux minutes : à l'heure dite, un message s'affiche dans la page.
- [ ] Après « Activer les notifications » et accord, une notification du navigateur apparaît aussi.
- [ ] Sans autorisation, le rappel apparaît dans l'Accueil avec le bouton « Vu ».
- [ ] Un rappel quotidien se reprogramme au lendemain après s'être déclenché.

## Sauvegarde et robustesse

- [ ] Réglages > Exporter mes données télécharge un fichier JSON.
- [ ] Réglages > Restaurer une sauvegarde : un résumé et une demande de confirmation s'affichent avant le remplacement.
- [ ] Restaurer un fichier texte quelconque renommé en `.json` : refus, données intactes.
- [ ] Recharger la page : toutes les données sont toujours là.

## Clavier et accessibilité

- [ ] `?` ouvre l'aide ; `1` à `8` changent de section ; `T` ouvre une nouvelle tâche ; `D` une nouvelle dépense ; `H` coche la prochaine habitude.
- [ ] Avec la touche Tab seule, on atteint tous les boutons, et celui qui a le focus est entouré.
- [ ] Échap ferme une fenêtre ouverte.

## Connexion (après les réglages Firebase et GitHub)

- [ ] « Se connecter avec GitHub » ouvre la fenêtre GitHub ; après accord, le nom et l'avatar s'affichent et l'indicateur passe à « Synchronisé ».
- [ ] Si des données locales existaient, le transfert vers le compte est proposé une seule fois. Après acceptation, elles sont visibles une fois connecté.
- [ ] Recharger la page : la session est conservée.
- [ ] « Se déconnecter » ramène au mode local.
- [ ] Dans la console Firebase, Firestore contient `users/{votre identifiant}/modules/` avec un document par module.

## Synchronisation entre deux appareils

- [ ] Se connecter avec le même compte sur l'ordinateur et sur le téléphone.
- [ ] Ajouter une tâche sur l'ordinateur : elle apparaît sur le téléphone en quelques secondes, sans recharger.
- [ ] Cocher une habitude sur le téléphone : elle est cochée sur l'ordinateur.
- [ ] Couper le réseau du téléphone (mode avion), ajouter une tâche : l'indicateur affiche « Hors ligne · 1 module en attente ».
- [ ] Rétablir le réseau : l'indicateur repasse à « Synchronisé » et la tâche apparaît sur l'ordinateur.
- [ ] Depuis une fenêtre de navigation privée, sans connexion au compte, vérifier qu'aucune donnée du compte n'est visible.
