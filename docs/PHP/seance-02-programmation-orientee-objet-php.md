
---

# 📘 Programmation Orientée Objet en PHP (OOP)

👨‍🏫 Responsable du module : **Reda Abdelhakmi**
📚 Module : **Introduction au Développement Web MVC**

---

# 🎯 Objectifs du cours

À la fin de ce cours, l’étudiant sera capable de :

✔ comprendre les principes de la **programmation orientée objet**

✔ créer des **classes et objets**

✔ utiliser **constructeur et destructeur**

✔ comprendre **encapsulation et héritage**

✔ utiliser **classe abstraite et interface

✔ comprendre le **polymorphisme**

✔ comprendre l’intérêt des **namespaces**

Ces concepts sont utilisés dans la majorité des frameworks modernes :

```
Symfony
Laravel
Spring
Django
```

---

# 🧠 Pourquoi la Programmation Orientée Objet ?

Dans les petits scripts PHP, on peut écrire du code simple :

```php
$nom = "Reda";
echo "Bonjour ".$nom;
```

Mais dans une grande application :

* il y a des centaines de fichiers
* plusieurs développeurs travaillent ensemble
* beaucoup de fonctionnalités

Sans structure, le code devient difficile à maintenir.

---

# 🎯 Objectifs de l’OOP

La Programmation Orientée Objet permet de :

✔ structurer le code
✔ réutiliser le code
✔ organiser les applications
✔ faciliter la maintenance

---

# 📦 Concept fondamental : Classe et Objet

Une **classe** est un **plan**.

Un **objet** est une **instance créée à partir de ce plan**.

---

# Schéma

```
Classe (Plan)

Etudiant
   │
   │ création
   ▼

Objet

etudiant1
etudiant2
etudiant3
```

---

# 🔹 Création d'une classe

```php
class Etudiant {

    public $nom;

}
```

Cette classe contient une propriété :

```
nom
```

---

# 🔹 Création d’un objet

```php
$e = new Etudiant();

$e->nom = "Reda";

echo $e->nom;
```

Résultat :

```
Reda
```

---

# 🔹 Les méthodes

Une **méthode** est une fonction définie dans une classe.

---

### Exemple

```php
class Etudiant {

    public $nom;

    public function saluer(){

        return "Bonjour ".$this->nom;

    }

}
```

---

### Utilisation

```php
$e = new Etudiant();

$e->nom = "Reda";

echo $e->saluer();
```

Résultat :

```
Bonjour Reda
```

---

# 🧠 Pourquoi utiliser des méthodes ?

Les méthodes permettent :

✔ d’ajouter des comportements aux objets
✔ de rendre le code plus lisible
✔ de regrouper les fonctionnalités

---

# 🔹 Le Constructeur

Le constructeur est une méthode appelée **automatiquement lors de la création d’un objet**.

Il permet **d’initialiser les propriétés**.

---

### Exemple

```php
class Etudiant {

    public $nom;

    public function __construct($nom){

        $this->nom = $nom;

    }

}
```

---

### Utilisation

```php
$e = new Etudiant("Reda");

echo $e->nom;
```

Résultat :

```
Reda
```

---

# 🔹 Le Destructeur

Le destructeur est appelé **lorsque l’objet est détruit**.

Il est utilisé pour :

* fermer une connexion
* libérer de la mémoire
* fermer un fichier

---

### Exemple

```php
class Test {

    public function __construct(){
        echo "Objet créé";
    }

    public function __destruct(){
        echo "Objet détruit";
    }

}
```

---

# 🔒 Encapsulation

L’encapsulation consiste à **protéger les données d’une classe**.

---

### Modificateurs d’accès

| mot clé   | signification                            |
| --------- | ---------------------------------------- |
| public    | accessible partout                       |
| private   | accessible uniquement dans la classe     |
| protected | accessible dans la classe et ses enfants |

---

### Exemple

```php
class Compte {

    private $solde = 0;

    public function deposer($montant){
        $this->solde += $montant;
    }

    public function getSolde(){
        return $this->solde;
    }

}
```

---

# 🧬 Héritage

L’héritage permet de **réutiliser le code d’une classe existante**.

---

### Exemple

```php
class Personne {

    public function parler(){
        echo "Je parle";
    }

}
```

Classe enfant :

```php
class Etudiant extends Personne {

}
```

---

### Utilisation

```php
$e = new Etudiant();

$e->parler();
```

---

# 🧠 Pourquoi utiliser l’héritage ?

✔ éviter la duplication du code
✔ créer une hiérarchie de classes
✔ faciliter l’évolution du code

---

# 🔹 Types d’héritage

## Héritage simple

```
A → B
```

Exemple :

```
Personne
   │
   ▼
Etudiant
```

✔ supporté par PHP
✔ utilisé dans Symfony

---

## Héritage multi-niveau

```
A → B → C
```

Exemple :

```
Personne
   │
   ▼
Etudiant
   │
   ▼
Doctorant
```

✔ supporté par PHP

---

## Héritage hiérarchique

```
      Personne
      /     \
 Etudiant  Professeur
```

✔ supporté par PHP

---

## Héritage multiple

```
A
B
 \
  C
```

❌ **Non supporté en PHP**

---

# 🔷 Classe abstraite

Une classe abstraite est une classe **qui ne peut pas être instanciée directement**.

Elle sert à définir une structure commune.

---

### Exemple

```php
abstract class Personne {

    public $nom;

    abstract public function role();

}
```

---

### Classe enfant

```php
class Etudiant extends Personne {

    public function role(){
        return "Je suis un étudiant";
    }

}
```

---

# 🔷 Interface

Une interface définit **un contrat**.

Elle impose certaines méthodes.

---

### Exemple

```php
interface Authentification {

    public function login();

    public function logout();

}
```

---

### Implémentation

```php
class User implements Authentification {

    public function login(){
        echo "Connexion utilisateur";
    }

    public function logout(){
        echo "Déconnexion utilisateur";
    }

}
```

---

# Différence

| Classe abstraite           | Interface                      |
| -------------------------- | ------------------------------ |
| peut contenir du code      | seulement signatures           |
| héritée avec extends       | implémentée avec implements    |
| une seule classe abstraite | plusieurs interfaces possibles |

---

# 🔷 Polymorphisme

Le polymorphisme signifie :

```
une même méthode peut avoir plusieurs comportements
```

---

### Exemple

```php
class Animal {

    public function parler(){
        echo "Je fais un bruit";
    }

}
```

Classe enfant :

```php
class Chat extends Animal {

    public function parler(){
        echo "Miaou";
    }

}
```

Classe enfant :

```php
class Chien extends Animal {

    public function parler(){
        echo "Wouf";
    }

}
```

---

### Utilisation

```php
$chat = new Chat();
$chien = new Chien();

$chat->parler();
$chien->parler();
```

---

# 📂 Namespace

Dans les grandes applications, plusieurs classes peuvent avoir le **même nom**.

Les **namespaces** permettent d’organiser le code.

---

### Exemple

```php
namespace App\Models;

class User {

}
```

Utilisation :

```php
use App\Models\User;

$user = new User();
```

---

# 🎯 Intérêt des namespaces

✔ éviter les conflits de noms
✔ organiser les classes
✔ structurer l’application

---

# Structure typique Symfony

```
App
 │
 ├── Controller
 ├── Entity
 ├── Repository
 └── Service
```

Chaque dossier correspond à un **namespace**.

---

# 🧪 Exercice 1 — Niveau simple

Créer une classe :

```
Personne
```

Propriétés :

```
nom
age
```

Méthode :

```
saluer()
```

Afficher :

```
Bonjour Reda
```

Ajouter un **constructeur** pour initialiser le nom.

---

# 🧪 Exercice 2 — Niveau avancé

Créer un mini système universitaire.

1️⃣ créer une **classe abstraite Personne**

Méthode :

```
role()
```

2️⃣ créer deux classes :

```
Etudiant
Professeur
```

3️⃣ créer une **interface Authentification**

Méthodes :

```
login()
logout()
```

4️⃣ implémenter l’interface dans :

```
User
```

5️⃣ créer un exemple de **polymorphisme** avec :

```
Animal
Chat
Chien
```

---

# ❓ Questions d’analyse

1️⃣ Quelle est la différence entre **classe et objet** ?

2️⃣ Pourquoi utilise-t-on **un constructeur** ?

3️⃣ Quelle est la différence entre **classe abstraite et interface** ?

4️⃣ Pourquoi les frameworks utilisent fortement **l’OOP** ?

---

# 🎓 Conclusion

Dans ce cours nous avons vu les concepts essentiels de la programmation orientée objet :

✔ classes et objets
✔ constructeur et destructeur
✔ encapsulation
✔ héritage
✔ classes abstraites
✔ interfaces
✔ polymorphisme
✔ namespaces

Ces concepts sont **la base des frameworks modernes comme Symfony**.

---

* création d’un **mini framework MVC pédagogique**
* compréhension des **routes comme dans Symfony**.
