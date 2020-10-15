# Composer

## Principe et fonctionnement

PHP pour faire du dev, c'est cool, mais comme tout language de programmation, il est pénible de coder des choses qui ont sûrement déjà été codées par d'autres (ex : traitement d'images, de formulaires, envoi de mails, génération de templates HTML, ...).

C'est là que Composer intervient ! Cet outil permet de distribuer son code sous forme de packages, et d'en télécharger pour les intégrer à notre code.

Dans chaque projet, vous pourrez retrouver un `composer.json` à la racine, qui continent la liste de tous les packages dont dépend le projet actuel, sous la forme `auteur/package`. La version du package à installer est déterminé comme suit : `"^2.7"` : installe le package avec la version la plus haute possible, mais au minimum là 2.7, `"5.1.*"` : installe la version la plus haute possible du package au sein de la version 5.1...

Les packages peuvent dépendre d'autres packages, eux-même avec des contraintes sur les versions. Quand on installe les packages, Composer calcule la combinaison ultime de tous les packages à installer avec la meilleure version pour chaque, qui réside dans le `composer.lock`. Quand on fait `composer install`, on installe exactement ce qui est spécifié dans ce fichier. `composer update` va mettre à jour la combinaison avec les packages les plus récents. En prod, il faut donc faire systèmatiquement `composer install` pour avoir des packages stables et éprouvés par les développeurs.

Il y a plusieurs blocs : require, et require-dev. En production, on installe uniquement les paquets nécessaires pour faire tourner l'application (`composer install --no-dev`), alors qu'en dev on installe tous les paquets, y compris ceux qui n'aident que les développeurs (débuggages, fixtures, ...) : `composer install`.

Pour installer un package, il suffit de taper : `composer require auteur/package [version]`.

## Stockage des paquets

Les fragments de codes distribués sous formes de packages sont installés dans le dossier `vendor` de votre projet.

Ce dossier est en général assez gros (il faut compter les dépendences directes mais aussi indirectes : les dépendances des dépendances), et il est résumé dans les fichiers `composer.json` et `composer.lock`. Ces deux fichiers suffisent, il suffit de faire `composer install`. **Il faut donc exclure le dossier `vendor` du repo git**, via le .gitignore, qui doit comprendre une ligne `/vendor/` signifiant que ce dossier est exclu.