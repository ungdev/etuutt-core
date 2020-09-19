# Configurer PHP sur son poste

## Installer mariadb

* Sous Linux, installer le paquet `mariadb`
* Sous Windows, aller sur [ce site](https://downloads.mariadb.org/) et installer la version 10.5 stable, et le fichier winx64.msi.
    * Cochez bien lors de l'installation `Modify root password` et notez le mdp créé (faites en un simple avec juste des chiffres et des lettres, il ne servira que sur votre poste). Décochez bien enable root access from remotes machines.
    * Cochez bien `Install as Service` et `Enable networking`

## Installer PHP

* Sur Linux :
    * `sudo add-apt-repository ppa:ondrej/php`
    * `sudo apt install php7.4 php7.4-pdo_mysql php7.4-mbstring`
* Sur Windows, cela se fait en plusieurs opérations.
    * Aller sur le [site suivant](https://windows.php.net/download), télécharger le zip (x64 non thread safe), et l'extraire dans un dossier à la racine de votre disque dur (par exemple `C:\dev-tools\php`). Vous devez donc avoir, à terme un fichier `php.exe` dans le dossier `C:\dev-tools\php`.
    * Téléchargez le [fichier suivant](https://curl.haxx.se/ca/cacert.pem) et placez le dans le même dossier que le php.exe
    * Dans ce dossier, vous devez copier le `php.ini-development` en `php.ini` (faites bien une copie afin de garder le fichier d'origine en cas de souci), puis ouvrez le avec VSCode (clic-droit, Ouvrir avec code) et changez les lignes suivantes :
    ```
    ;  Remplacer
    ;curl.cainfo =
    ;  par (sans le point virgule)
    curl.cainfo = "C:\dev-tools\php\cacert.pem"

    ;  Remplacer
    ;openssl.capath =
    ;  par (sans le point virgule)
    openssl.capath = "C:\dev-tools\php\cacert.pem"
    ```
    * Toujours dans le php.ini, recherchez `Dynamic Extensions`, puis décommentez (enlevez le `;`) des lignes suivantes :
    ```
    extension=curl
    extension=fileinfo
    extension=mbstring
    extension=pdo_mysql
    ```
    * Recherchez également la ligne `;extension_dir = "ext"` pour la décommenter (enlevez le `;` devant)
    * Il faut ensuite, dans la barre des tâches, rechercher `path` et ouvrir `Modifier les variables d'environnement`, puis recliquez sur le bouton du bas `Variables d'environnement` puis dans `Variables systèmes`, double cliquer sur la variable `Path` puis cliquer sur `Nouveau` et indiquer `C:\dev-tools\php\` en ajoutant bien le `\` à la fin. Puis valider la saisie en appuyant sur entrée puis en cliquant sur ok.

## Installer composer
* Sous linux : avec votre gestionnaire de paquet : `sudo apt install composer`
* Sous Windows en utilisant [l'installateur prévu à cet effet](https://getcomposer.org/Composer-Setup.exe).

## Installer l'exécutable Symfony
* Linux : `wget https://get.symfony.com/cli/installer -O - | bash && sudo mv symfony /usr/bin/symfony`
* Windows : allez sur le [site de Symfony](https://symfony.com/download) pour télécharger l'installateur.

## Installer PHPStorm

Etape finale !

PHPStorm est un des meilleurs (si ce n'est pas le meilleur) IDE pour développer en PHP. C'est celui que je recommande, mais VSCode avec des extensions peut très bien le faire, tout comme Atom, Vim, ... Chacun son chemin, chacun son destin !

* Se connecter à Jetbrains avec le Github Student Pack [ici](https://www.jetbrains.com/shop/eform/students), indiquez une date approximative de diplomation pour , vous devrez ensuite vous créer un compte.
* Téléchargez ensuite la [Jetbrains Toolbox](https://www.jetbrains.com/toolbox-app/)
* Depuis la JetBrains Toolbox, installez ensuite PHPStorm
* Au premier lancement, Jetbrains va vous demander plusieurs choses, notamment les plugins. Installez bien les plugins :
    * .env
    * EditorConfig
    * Ideolog
    * Symfony