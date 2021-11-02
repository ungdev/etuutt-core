# Configuration

Ce dossier contient des instructions afin de préparer ton poste. De manière générale, il est recommandé d'utiliser Linux, la configuration est beaucoup plus simple. Mais sous Windows, ça marche très bien aussi en suivant les étapes indiquées après !

## Créez-vous un compte Github

Vous êtes dessus, cliquez sur `Sign Up` en haut à droite.

Activez le [Github Student Pack](https://education.github.com/pack) en cliquant sur le bouton "Get your pack" et en fournissant votre mail universitaire (UTT, ...)

## Configuration commune à tous les projets

### Installer VSCode

Visual Studio Code est un éditeur de texte brut. Il est très pratique pour éditer rapidement un fichier de configuration. Vous êtes bien entendu libre d'utiliser autre chose (Notepad++, Vim, ...) mais n'utilisez **jamais** Office ou LibreOffice pour éditer un fichier, ils n'éditent pas de manière **brute** les fichiers, ils ajoutent des informations supplémentaires (mise en forme, ...) qui rendent ces fichiers inutilisables dans notre contexte.

Allez sur [le site de VSCode](https://code.visualstudio.com/), téléchargez et installez la version correspondant à votre PC.

- Pour Windows, laissez toutes les options par défaut mais pensez à cocher toutes les cases du genre `Ajouter VSCode au menu contextuel`
- Pour Linux, vscode n'est pas directement accessible dans les repos traditionnels, il faut donc le télécharger et l'installer via votre gestionnaire de paquets (afin d'ajouter aussi le repo dans la liste de vos sources pour les mises à jour), par exemple `sudo apt install ./vscode.deb`.

### Installer git

C'est un outil qui va te permettre de télécharger et d'envoyer du code source.

- Sur windows, il faut se rendre sur [ce site](https://gitforwindows.org/), cliquer sur download. Vous arrivez sur la page des releases du projet Github correspondant. Plus bas, dans assets, téléchargez le fichier exe en 64bits puis installez le sur votre poste, en **laissant les options par défaut**.
- Sur Linux, c'est beaucoup plus facile. Installez le paquet `git` avec votre gestionnaire de paquets (exemple : `sudo apt install git`).

### Installer commitizen

C'est un outil qui va te permettre d'expliquer aux autres collaborateurs ce que tu as changé sur le code quand tu as fait une modification de manière standard.

Il faut d'abord installer node.

- Sous Windows, il faut aller sur [ce site](https://nodejs.org/en/), télécharger la version current et installer en laissant les options standards.
- Sous Linux, avec le gestionnaire de paquet, installer `npm`, soit par exemple `sudo apt install npm`

Ensuite il faut installer commitizen, pour cela, ouvrez un terminal et saisissez : `npm install -g commitizen` puis `npm install -g cz-conventional-changelog` puis `npm install -g cz-emoji`.

## Configuration spécifique à PHP

Aller dans le dossier PHP

## Configuration spécifique au Front

Aller dans le dossier [FRONT](FRONT/)
