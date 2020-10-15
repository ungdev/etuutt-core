# Symfony

Symfony fournit un cadre de travail qui facilite la vie des développeurs web, avec, entre autres :
* Connexion simplifiée à la base de données via Doctrine
* Gestion des formulaires
* Templates pour l'affichage
* Sécurité / Authentification
* Gestion de la session utilisateur
* Templating HTML puissant via Twig
* Permet de relier très facilement des routes (url) à des fonctions renvoyant des données (HTML, json, ...)

## Framework MVC

Symfony est un framework dit MVC car il permet de définir et relier :
* **M**odèles. Ce sont des représentations informatiques d'objets de la vie courante (utilisateur, association, évènement, cours, ...). Ces modèles sont aussi appelés Entités. Symfony, via Doctrine, fournit des commandes simples et efficaces pour gérer ces identités, comme décrit dans le fichier [entities.md](entities.md) ou sur [la doc officielle](https://symfony.com/doc/current/doctrine.html).
* **V**ues. C'est ce qui est renvoyé à l'utilisateur (HTML)
* **C**ontrolleurs. C'est le lien entre les modèles et les vues, c'est là que se fait la logique qui permet à un utilisateur qui saisit une URL de recevoir une réponse.

## Doc générale

[6 étapes pour comprendre comment Symfony fonctionne](https://symfony.com/doc/current/setup.html)

* Exemples de projets Symfony 5 :
    *  Une appli de sondage connectée au site etu : https://github.com/larueli/kimanj
    * Une appli de gestion de stock : https://github.com/larueli/stock