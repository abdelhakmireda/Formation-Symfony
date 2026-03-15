
# 📘 Séance 03 — Introduction à l’architecture MVC

👨‍🏫 Responsable du module : **Reda Abdelhakmi**
📚 Module : **Introduction au Développement Web MVC**

---

# 🎯 Objectifs pédagogiques

À la fin de cette séance, l’étudiant sera capable de :

✔ comprendre pourquoi il faut organiser le code PHP
✔ comprendre le principe de l’architecture **MVC**
✔ distinguer les rôles de **Model, View et Controller**
✔ comprendre la structure simple d’un projet MVC

Cette séance est une **introduction progressive** avant de créer un mini framework MVC.

---

# 🧠 1 — Le problème du PHP non structuré

Dans les premiers programmes PHP, on écrit souvent tout dans un seul fichier.

Exemple :

```php
<?php

$nom = "Sara";

echo "<h1>Bonjour ".$nom."</h1>";

?>
```

Ce type de script fonctionne bien pour un petit programme.

Mais dans un vrai site web :

* plusieurs pages
* beaucoup de fonctionnalités
* plusieurs développeurs
* connexion à une base de données

Le code devient :

❌ difficile à lire
❌ difficile à modifier
❌ difficile à maintenir

Il faut donc **organiser le code**.

---

# 🎯 Solution : l’architecture MVC

Pour organiser les applications web, on utilise souvent **MVC**.

MVC signifie :

**Model — View — Controller**

Cette architecture est utilisée dans de nombreux frameworks :

* Symfony
* Laravel
* Ruby on Rails
* Django

---

# 🧩 2 — Principe du MVC

MVC consiste à **séparer le programme en trois parties**.

| Composant  | Rôle               |
| ---------- | ------------------ |
| Model      | gérer les données  |
| Controller | gérer la logique   |
| View       | afficher les pages |

Cette séparation permet de rendre le code **plus clair et mieux organisé**.

---

# 📊 Fonctionnement du MVC

Lorsqu’un utilisateur visite une page web :

1️⃣ Le **Controller** reçoit la demande
2️⃣ Le **Model** fournit les données
3️⃣ La **View** affiche les données

Schéma simplifié :

```
Utilisateur
     │
     ▼
Controller
     │
     ▼
Model
     │
     ▼
Controller
     │
     ▼
View
     │
     ▼
Navigateur
```

---

# 🔹 3 — Le Model

Le **Model** représente les données de l’application.

Exemple :

```php
<?php

class Etudiant {

    public function getEtudiants(){

        return ["Sara", "Ali", "Karim"];

    }

}

?>
```

Cette classe retourne une liste d’étudiants.

Dans une vraie application, le Model peut récupérer les données depuis :

* une base de données
* une API
* un fichier

---

# 🔹 4 — Le Controller

Le **Controller** est responsable de la logique du programme.

Il :

* appelle le Model
* récupère les données
* envoie les données à la View

Exemple :

```php
<?php

class EtudiantController {

    public function index(){

        $model = new Etudiant();

        $etudiants = $model->getEtudiants();

        require "views/etudiants.php";

    }

}

?>
```

---

# 🔹 5 — La View

La **View** affiche les informations.

Elle contient principalement :

* HTML
* un peu de PHP

Exemple :

```php
<h1>Liste des étudiants</h1>

<ul>

<?php foreach($etudiants as $e){ ?>

<li><?= $e ?></li>

<?php } ?>

</ul>
```

Cette page affiche la liste des étudiants.

---

# 📂 6 — Structure simple d’un projet MVC

Organisation des fichiers :

```
project/

index.php

models
    Etudiant.php

controllers
    EtudiantController.php

views
    etudiants.php
```

Chaque dossier a un rôle :

| Dossier     | Contenu                     |
| ----------- | --------------------------- |
| models      | les classes de données      |
| controllers | la logique de l'application |
| views       | les pages HTML              |

---

# 🔄 7 — Cycle d’une requête

Lorsqu’un utilisateur visite une page :

1️⃣ le **Controller** est exécuté
2️⃣ le Controller demande les données au **Model**
3️⃣ le Model retourne les données
4️⃣ la **View** affiche les données

Ce fonctionnement permet de **séparer les responsabilités** dans l’application.

---

# 🧪 Exercices

## Exercice 1

Créer une classe :

```
Produit
```

Créer une méthode :

```
getProduits()
```

Retourner :

```
ordinateur
clavier
souris
```

---

## Exercice 2

Créer un **ProduitController**

Afficher les produits dans une **View**.

---

# ❓ Questions d’analyse

1️⃣ Que signifie MVC ?

2️⃣ Quel est le rôle du **Model** ?

3️⃣ Quel est le rôle du **Controller** ?

4️⃣ Pourquoi sépare-t-on le code en Model, View et Controller ?

---

# 🎓 Conclusion

Dans cette séance nous avons découvert :

✔ le problème du code PHP non organisé
✔ le principe de l’architecture MVC
✔ le rôle du **Model, View et Controller**
✔ la structure simple d’un projet MVC

Ces concepts sont **la base des frameworks modernes comme Symfony et Laravel**.

---

