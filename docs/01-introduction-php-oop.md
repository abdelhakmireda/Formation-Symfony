# 01 - Introduction à PHP et à la Programmation Orientée Objet (OOP) 🚀

## Objectifs de ce chapitre 🎯
Dans ce chapitre, nous allons découvrir les bases de PHP et les concepts clés de la Programmation Orientée Objet (OOP) 💻, qui sont essentiels pour travailler avec Symfony.

## Qu'est-ce que PHP ? 🤔
PHP (Hypertext Preprocessor) est un langage de programmation côté serveur utilisé pour générer du contenu dynamique sur le web. Avec des frameworks comme Symfony, PHP permet de créer des applications web puissantes et modulaires.

## Les bases de PHP ⚙️

### Variables et types de données 🔢
Les variables sont utilisées pour stocker des informations. PHP prend en charge plusieurs types de données comme les chaînes de caractères, les entiers, les tableaux, etc.

Exemple :
```php
$nom = "Symfony"; // Chaîne de caractères
$age = 3;         // Entier
```
Retour :
$nom contient "Symfony" et $age contient l'entier 3.

### Structures de contrôle 📝
Les structures de contrôle permettent de manipuler le flux d'exécution du programme.

Exemple :
```php
if ($age >= 18) {
    echo "Vous êtes majeur";
}
```
Retour :
Si $age est supérieur ou égal à 18, le message "Vous êtes majeur" sera affiché.

### Fonctions 🔧
Les fonctions organisent et réutilisent du code.

Exemple :
```php
function saluer($nom) {
    return "Bonjour, $nom!";
}

echo saluer("Alice");
```
Retour :
Cela affichera "Bonjour, Alice!" sur la page.

## Qu'est-ce que la Programmation Orientée Objet (OOP) ? 🏗️
L'OOP est un modèle de programmation qui organise le code autour des objets. Ces objets contiennent des propriétés (variables) et des méthodes (fonctions). L'OOP permet de structurer l'application de manière plus lisible, maintenable et évolutive.

## Concepts clés de l'OOP 🔑

### Classe et Objet 🏷️
Une classe est un modèle pour créer des objets. Un objet est une instance d'une classe.

Exemple :
```php
class Personne {
    public $nom;
    public $age;

    public function __construct($nom, $age) {
        $this->nom = $nom;
        $this->age = $age;
    }

    public function saluer() {
        return "Bonjour, je m'appelle $this->nom et j'ai $this->age ans.";
    }
}

$personne = new Personne("Alice", 30);
echo $personne->saluer();  // "Bonjour, je m'appelle Alice et j'ai 30 ans."
```
Retour :
L'objet Personne affiche un message saluant l'utilisateur avec son nom et son âge.

### Encapsulation 🛡️
L'encapsulation permet de cacher les détails internes d'un objet et de fournir des méthodes pour accéder à ces données de manière contrôlée.

Exemple :
```php
class CompteBancaire {
    private $solde;

    public function __construct($soldeInitial) {
        $this->solde = $soldeInitial;
    }

    public function depot($montant) {
        $this->solde += $montant;
    }

    public function getSolde() {
        return $this->solde;
    }
}

$compte = new CompteBancaire(1000);
$compte->depot(500);
echo $compte->getSolde();  // 1500
```
Retour :
La classe CompteBancaire gère l'accès au solde de manière sécurisée.

### Héritage 👑
L'héritage permet de créer une nouvelle classe à partir d'une classe existante, tout en réutilisant ses méthodes et propriétés.

Exemple :
```php
class Employe extends Personne {
    private $poste;

    public function __construct($nom, $age, $poste) {
        parent::__construct($nom, $age);
        $this->poste = $poste;
    }

    public function afficherPoste() {
        return "$this->nom occupe le poste de $this->poste.";
    }
}

$employe = new Employe("Bob", 28, "Développeur");
echo $employe->afficherPoste();  // "Bob occupe le poste de Développeur."
```
Retour :
L'objet Employe hérite des propriétés et méthodes de Personne.

### Polymorphisme 🔄
Le polymorphisme permet d'utiliser la même méthode dans différentes classes avec des comportements différents.

Exemple :
```php
class Animal {
    public function parler() {
        echo "Je fais un bruit";
    }
}

class Chat extends Animal {
    public function parler() {
        echo "Miaou!";
    }
}

class Chien extends Animal {
    public function parler() {
        echo "Wouf!";
    }
}

$chat = new Chat();
$chat->parler();  // "Miaou!"

$chien = new Chien();
$chien->parler();  // "Wouf!"
```
Retour :
La méthode parler() produit un comportement spécifique en fonction de la classe (chat ou chien).

### Interfaces et Classes Abstraites 📜

#### Interface 🖥️
Une interface définit un contrat que les classes doivent suivre. Elle ne peut pas contenir de logique mais seulement des signatures de méthodes.

Exemple :
```php
interface Vehicule {
    public function demarrer();
}

class Voiture implements Vehicule {
    public function demarrer() {
        echo "La voiture démarre";
    }
}

class Moto implements Vehicule {
    public function demarrer() {
        echo "La moto démarre";
    }
}

$voiture = new Voiture();
$voiture->demarrer();  // "La voiture démarre"
```
Retour :
Chaque classe qui implémente l'interface Vehicule doit définir la méthode demarrer().

#### Classe Abstraite 🏛️
Une classe abstraite peut contenir des méthodes avec ou sans implémentation. Elle ne peut pas être instanciée directement.

Exemple :
```php
abstract class Animal {
    abstract public function parler();

    public function dormir() {
        echo "Je dors";
    }
}

class Chat extends Animal {
    public function parler() {
        echo "Miaou!";
    }
}

$chat = new Chat();
$chat->parler();  // "Miaou!"
```
Retour :
La classe Chat hérite de la méthode dormir() de Animal et implémente la méthode parler().

### use et les namespaces 📂
Le namespace permet de regrouper les classes, interfaces et fonctions sous un même espace, évitant ainsi les conflits de noms. Grâce à `use`, tu peux importer une classe ou un namespace dans un fichier pour l'utiliser sans avoir à spécifier son chemin complet.

Exemple :
```php
namespace App\Models;

class Utilisateur {
    public function afficher() {
        echo "Utilisateur affiché";
    }
}
```
Dans un autre fichier, tu peux l'importer ainsi :
```php
use App\Models\Utilisateur;

$utilisateur = new Utilisateur();
$utilisateur->afficher();  // "Utilisateur affiché"
```

## Conclusion 🎉
Dans ce chapitre, nous avons couvert les bases de PHP ainsi que les concepts fondamentaux de la Programmation Orientée Objet (OOP). Nous avons exploré les éléments essentiels comme les classes, objets, encapsulation, héritage, polymorphisme, et la différence entre interfaces et classes abstraites.

Ces concepts sont la base pour développer des applications robustes et maintenables avec PHP et Symfony. Dans les prochains chapitres, nous approfondirons l’utilisation de Symfony et les bonnes pratiques pour structurer une application web professionnelle.
