# Ajouter un repo

Imaginons que nous devions ajouter une API, ou un nouveau repo de manière générale. Voici les étapes et conventions à suivre.

## Nommage, stockage et accès

* Le nom du repo et du projet sera sous la forme suivante : `etuutt-service`, en **minuscule**.
* Le repo est créé dans github, sur l'organisation `ungdev`. Le repo doit être créé complètement vide.
* Au niveau des droits d'accès au repo, il y a plusieurs équipes. Selon votre projet, il faudra en créer une ou incorporer les droits d'une équipe existante. L'équipe d'amdin (`etuutt-admin`) vous indiquera s'il faut créer une équipe et quelle équipe il faudra créer le cas échéant. S'il doit y avoir une nouvelle équipe spécifique à votre projet, celle-ci doit impérativement porter le nom `etuutt-service` et avoir comme équipe parente `etuutt`.
* Les droits sont les suivants :
    * L'équipe `etuutt` a les droits `Triage`.
    * Votre équipe ou une équipe déjà existante, rattachée au projet, a les droits `Maintain`.
    * L'équipe `etuutt-admin` a les droits `Admin`.

## Convention communes aux repos

* Utilisation de [conventional commits](https://www.conventionalcommits.org/en/v1.0.0/). Le mieux est d'utiliser [commitizen](https://github.com/commitizen/cz-cli#conventional-commit-messages-as-a-global-utility) en l'installant sur son poste (indépendant du projet). Dans le dossier du projet, taper la commande `echo '{ "path": "cz-emoji" }' > .czrc` afin de définir l'adaptateur pour le projet.
* Le projet est sous [licence MIT](https://choosealicense.com/licenses/mit/), attribué à `UTT NET GROUP`.
* Un dossier `docs` est à la racine. Le dossier docs de la branche master est utilisé pour Github Pages.
* Deux branches : `prod` et `dev`. La branche par défaut est `dev`.

* Pour du back, on utilise PHP/Symfony
* Le front est en React

## Appli PHP

* `symfony new etuutt-service --full`
* `cd etuutt-service`
* `git branch -m master prod`
* `echo 7.4 > .php-version`
* Installation d'outils de dev supplémentaires
```
composer require --dev phpmd/phpmd
composer require --dev friendsofphp/php-cs-fixer
composer require --dev doctrine/doctrine-fixtures-bundle
composer require --dev squizlabs/php_codesniffer
```

Vous devez copier le `.php_cs.dist` et le `.travis.yml` du dossier php et le mettre à la racine de votre projet.




