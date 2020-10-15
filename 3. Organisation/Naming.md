# Conventions de nommage

Comment choisir ses noms pour ses variables ?

## Quelques conventions

Plusieurs conventions existent :
* camelCase : `maVariable`. Tous les mots attachés, première lettre de chaque mot en majuscule, sauf la première lettre.
* PascalCase : `MaVariable`. Comme le camelCase, mais première lettre en majuscule.
* snake_case : `ma_variable`. Tous les mots en minuscule, séparés par des underscores
* SCREAMING_SNAKE_CASE : `MA_VARIABLE`. Comme snake_case, mais en majuscule.
* kebab-case : `ma-variable`. Tous les mots en minuscules, séparés par des tirets.

## Pour notre projet

* Nom de classe : PascalCase. Attention, en PHP, une seule classe par fichier, et le fichier doit porter le même nom que la classe suffixé par `.php`.
* Constante globale : SCREAMING_SNAKE_CASE
* Variables d'environnement : SCREAMING_SNAKE_CASE
* Nom d'une variable : camelCase
* Tout ce qui touche de près à la BDD ou les formulaires Symfony (requêtes directes) écrites en snake case

## Petits tips dans notre projet

* Les classes controllers Symfony doivent toujours se terminer par `Controller`
* Les classes formulaires en Symfony doivent toujours se terminer par `Type`. De l'extérieur, ces formulaires peuvent être remplis via une requete POST x-www-form-urlencoded avec dans le body les champs de type nom_formulaire_sans_type[champ].

## Linting

Nous avons plusieurs manières syntaxiques d'écrire notre code (mettre des espaces, des sauts de ligne, des commentaires, ...). Afin d'être sûr que le code soit homogène, on utilise du linting. C'est un processus (souvent via un outil dédié) qui vérifie que le code que vous avez envoyé correspond aux conventions du projet.

### Php Coding Standards Fixer

Pour Php, nous utilisons php-cs-fixer, il permet à la fois de vérifier du code, mais aussi de corriger automatiquement le code pour suivre la convention ! Il se présente sous la forme d'un [package composer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) (installé dans tous les projets etuutt-* du back).

Les conventions suivies sont définies à la racine du projet dans le fichier `.php_cs.dist`. Les conventions (ou ruleset) sont [listées ici](https://mlocati.github.io/php-cs-fixer-configurator/#version:2.16) (en haut à droite, set). Les conventions dites risky peuvent casser le code en modifiant son sens, mais dans des cas très particuliers.

Les conventions suivies pour le back sont les conventions/ruleset :

* Symfony (y compris risky)
* PhpCsFixer (y compris risky)
* DoctrineAnnotation
* PSR1
* PSR2
* Syntaxe courte des tableaux (utiliser les crochets et non `array()`)

Nous suivons aussi la convention [PSR4](https://www.php-fig.org/psr/psr-4/), mais pas besoin de la vérifier sinon le code ne fonctionne pas de base (car indispensable pous Symfony), ce n'est donc plus de l'ordre du linting. Cette convention permet de trouver rapidement où sont les classes en les chargeant automatiquement directement depuis les fichiers sources et en les faisant correspondre automatiquement aux espaces de noms associés.

Une commande à retenir pour adapter automatiquement son code : `php vendor/bin/php-cs-fixer fix src`. On appelle l'exécutable du package (dans le dossier vendor) et on lui dit de réparer le contenu du dossier src. Vous devez le faire avant chaque commit !

Une pull request dont le linting n'est pas correct sera bloqué automatiquement, car Travis, notre outil d'intégration continue (concept d'intégrer des petits morceaux de code régulièrement dans le code source complet en vérifiant régulièrement sa qualité) vérifie de son côté que les ruleset sont appliqués (cf le fichier `.travis.yml` à la racine du dossier).

D'autres outils existent, comme Php CodeSniffer ou Php Mess Detector, mais nous ne les utilisons pas encore pour le moment.