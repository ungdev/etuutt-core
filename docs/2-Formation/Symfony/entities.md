# Les entités en Symfony

## Les entités

### Une entité, quésako ?

Une entité, c'est une classe / un objet. Pour ceux qui ne connaissent pas la programmation orientée objet, voici les grandes lignes :
* Tout est décrit par des objets / classes / modèles / entités (termes plus ou moins équivalents)
* Un objet (exemple : une voiture) contient plusieurs choses :
    * Des propriétés : ce sont des variables spécifiques à l'objet (exemple : vitesse, nombre de places disponibles, dégâts, ...). Bref, tout ce qui décrit l'objet.
    * Des méthodes : ce sont des actions que peut faire l'objet, décrites sous la forme de fonctions. Exemple : `ajouterPassager(mailPassager)`. Cette fonction vérifie le nombre de places encore disponible, diminuera le nombre de place de la voiture de 1, envoie un mail au nouveau passager et renvoie `True` s'il y avait encore assez de place pour ce passager.
* Un objet représente parfois quelque chose qui existe dans la vraie vie (un évènement, une association, un utilisateur, ...) et qui doit être stocké dans la base de données. Dans ce cas, il s'agit spécifiquement d'une entité (terminologie Symfony).

### Instancier une entité et accéder à ses composantes

* Votre objet / classe est purement théorique. Pour créer réellement une voiture, il faut instancier la classe correspondante. En PHP, on utilise le mot clef `new`, vous pourrez ensuite accéder aux composantes de cette manière : 
```
$maVoiture = new Voiture();
$maVoiture->vitesse = 20;
$maVoiture->placesDisponibles = 4;
$maVoiture->ajouterPassager("jean@dupont.fr");
```

* Chaque méthode ou propriété a une visibilité. Si la variable ou méthode est déclarée privée, on ne peut pas y accéder de l'extérieur, exemple, si je définis la variable vitesse comme privée, je ne pourrai pas utiliser `$maVoiture->vitesse;`. On peut en revanche créer une méthode publique `getVitesse()` et `setVitesse(vitesse)` qui vont respectivement renvoyer la vitesse et définir la vitesse. L'avantage, c'est que l'on peut définir une logique ! On pourrait imaginer une vérification systématique qu'on ne dépasse pas une vitesse max en fixant la vitesse : cela se fera dans la fonction `setVitesse`. Ces fonctions publiques qui servent à modifier ou récupérer la valeur d'un attribut privé sont appelées les getters et setters. C'est le comportement par défaut d'une entité en Symfony.

### Les namespaces

### Pour aller plus loin

* Par convention (PSR4) :
    * une seule classe par fichier
    * si la classe s'appelle Voiture, le fichier associé doit s'appeller `Voiture.php`
* En général on utilise PascalCase pour les noms de classes et camelCase pour les propriétés et méthodes (voir la section organisation).
* Bizarre, `$maVoiture = new Voiture()`, on dirait que Voiture est une fonction qui peut prendre des paramètres ? En fait, vous pouvez définir une méthode `__construct(param1, param2, ...)` (avec deux `_`) qui va réaliser des actions par défaut quand vous allez instancier votre classe, comme mettre la vitesse à 0 pour notre voiture, lui fixer un nom directement, ...
* On ne copie pas facilement une entité.
```
$maClio = new Voiture();
$maClio->vitesse = 50;
$monKangoo = $maClio; // copie ?
$monKangoo->vitesse = 20;

$monKangoo->vitesse; // 20
$maClio->vitesse; // 20 aussi...
```
En fait, c'est comme un tableau. La variable contient simplement une référence vers l'instance de l'objet. Copier la variable, c'est juste copier la référence. Pour plus d'infos, renseignez-vous sur les deep copy.

## Les entités en Symfony

Une entité en Symfony est une entité particulière car elle est interprétée de façon à ce que chacune de ses instances puisse être stockée dans une base de données.

**Lisez la documentation Symfony sur le sujet !** [https://symfony.com/doc/current/doctrine.html](https://symfony.com/doc/current/doctrine.html)

### Base de donnée ?

Pour la faire très courte : une base de donnée SQL, c'est comme un grand classeur excel, avec plusieurs feuilles, nos données sont stockées sur les lignes. Notre application est dans une base de données contenant plusieurs tables (feuilles), et chaque table correspond à une entité, les colonnes correspondant aux noms des propriétés. SQL définit aussi une syntaxe permettant de manipuler les entrées / tables / ...

Avant, il fallait programmer la liaison vers la BDD à la main, manuellement créer les entrées dans la BDD, programmer en SQL, ...
Aujourd'hui, Doctrine est le composant qui fait cette liaison avec PHP, et en règle générale on n'a même plus de SQL à taper.

Doctrine est appelé via des annotations qui sont des fragments de code dans des commentaires (oui oui vous avez bien lu, même les commentaires sont interprétés, s'ils commencent par @ !). Si, dans une classe du namespace App\Entity, il y a des annotations faisant référence à Doctrine, un stockage dans la BDD est prévu.

Note : on verra parfois le sigle DB pour parler des BDD. C'est enfaite l'abréviation de "DataBase", pour nos camarades anglophones.

```
<?php

namespace App\Entity;

use App\Repository\UserRepository;
use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity(repositoryClass=UserRepository::class)
 */
class User
{
    /**
     * @ORM\Id
     * @ORM\GeneratedValue
     * @ORM\Column(type="integer")
     */
    private $id;

    /**
     * @ORM\Column(type="string", length=255)
     */
    private $casUid;

    /**
     * @ORM\Column(type="integer", nullable=true)
     */
    private $userId;

    /**
     * @ORM\Column(type="string", length=255, nullable=true)
     */
    private $ldapUNGUid;

    // getters et setters
}
```

Une commande toute prête permet de manipuler les entités : `php bin/console make:entity`. Vous pouvez aussi faire des relations entre entités. Tout est détaillé dans la documentation.

## Dans le code source

Pour stocker une entité :
```
// Création ou récupération
$maVoiture = new Voiture();
$maVoiture $entityManager->getRepository(Voiture::class)->find(5);

// Modification
$maVoiture->setVitesse(50);

// Stockage après création ou modification
$entityManager->persist($maVoiture);

//Suppression
$entityManager->remove($maVoiture);

// Enregistrement des modifications
$entityManager-flush();
```