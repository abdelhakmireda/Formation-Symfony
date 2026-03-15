

# 📘 Séance 04 — Navigation entre pages et contrôleurs en MVC

👨‍🏫 Responsable du module : **Reda Abdelhakmi**
📚 Module : **Introduction au Développement Web MVC**

---

# 🎯 Objectifs pédagogiques

À la fin de cette séance, l’étudiant sera capable de :

✔ comprendre comment naviguer entre plusieurs pages dans une application MVC
✔ comprendre le rôle du fichier **index.php** dans une application
✔ appeler différents **controllers** selon la page demandée
✔ créer une petite application MVC avec plusieurs pages

Cette séance permet de mieux comprendre **comment une application web organise ses pages**, avant d’utiliser un framework comme **Symfony**.

---

# 🧠 1 — Ajouter plusieurs pages dans une application MVC

Dans la séance précédente, nous avons affiché une seule page :

```id="x2q1w9"
Liste des étudiants
```

Mais un site web contient généralement plusieurs pages :

* Accueil
* Produits
* Contact
* A propos

Nous devons donc organiser **la navigation entre les pages**.

---

# 🌐 2 — Exemple de pages dans un site web

Imaginons un petit site :

| Page     | Description        |
| -------- | ------------------ |
| Accueil  | page principale    |
| Produits | liste des produits |
| Contact  | page de contact    |

Chaque page sera gérée par un **Controller**.

---

# 📂 Structure du projet

Notre projet MVC peut être organisé ainsi :

```id="ql37qk"
project/

index.php

models
    Produit.php

controllers
    HomeController.php
    ProduitController.php

views
    home.php
    produits.php
```

---

# 🔹 3 — Le rôle du fichier index.php

Le fichier **index.php** est souvent la **page principale du site**.

Il peut servir à :

✔ recevoir la demande de l’utilisateur
✔ décider quel controller doit être exécuté

---

# Exemple simple de index.php

```php
<?php

require "controllers/HomeController.php";
require "controllers/ProduitController.php";

$page = $_GET['page'] ?? "home";

if($page == "home"){

    $controller = new HomeController();
    $controller->index();

}

if($page == "produits"){

    $controller = new ProduitController();
    $controller->index();

}

?>
```

Explication :

* `$_GET['page']` récupère la page demandée
* selon la valeur, on appelle un controller

---

# 🔹 4 — HomeController

Fichier :

```id="o8c2u7"
controllers/HomeController.php
```

```php
<?php

class HomeController {

    public function index(){

        require "views/home.php";

    }

}

?>
```

---

# 🔹 5 — View de la page d'accueil

```id="y92n0p"
views/home.php
```

```html
<h1>Bienvenue sur notre site</h1>

<p>Ceci est la page d'accueil.</p>

<a href="index.php?page=produits">Voir les produits</a>
```

Ce lien permet d’aller vers la page **produits**.

---

# 🔹 6 — ProduitController

```id="ib41rt"
controllers/ProduitController.php
```

```php
<?php

class ProduitController {

    public function index(){

        $produits = ["ordinateur","clavier","souris"];

        require "views/produits.php";

    }

}

?>
```

---

# 🔹 7 — View produits

```id="5qq2vy"
views/produits.php
```

```php
<h1>Liste des produits</h1>

<ul>

<?php foreach($produits as $p){ ?>

<li><?= $p ?></li>

<?php } ?>

</ul>

<a href="index.php?page=home">Retour à l'accueil</a>
```

---

# 🔄 8 — Fonctionnement de la navigation

Lorsque l’utilisateur clique sur :

```id="3u6m6y"
index.php?page=produits
```

les étapes sont :

1️⃣ le navigateur ouvre `index.php`
2️⃣ `index.php` lit la variable `page`
3️⃣ `ProduitController` est appelé
4️⃣ la view `produits.php` est affichée

---

# 📊 Schéma du fonctionnement

```id="13ewq1"
Utilisateur
     │
     ▼
index.php
     │
     ▼
Controller
     │
     ▼
Model (si nécessaire)
     │
     ▼
View
     │
     ▼
Page affichée
```

---

# 🎯 Pourquoi cette organisation est importante ?

Cette organisation permet :

✔ un code mieux structuré
✔ une séparation des responsabilités
✔ une application plus facile à maintenir

C’est exactement le principe utilisé dans les frameworks modernes.

---

# 🔍 Comparaison avec Symfony

| Concept         | Dans notre projet | Dans Symfony       |
| --------------- | ----------------- | ------------------ |
| Page principale | index.php         | public/index.php   |
| Controller      | classes PHP       | Controller Symfony |
| View            | HTML / PHP        | Twig               |
| Navigation      | $_GET             | Routing Symfony    |

---

# 🧪 Exercices

### Exercice 1

Ajouter une nouvelle page :

```id="0t9l9b"
about
```

Afficher :

```id="rvq86x"
Page à propos
```

---

### Exercice 2

Créer un controller :

```id="o0chd4"
ContactController
```

Afficher :

```id="v0j0qg"
Contactez-nous
```

---

### Exercice 3

Ajouter un lien de navigation :

```id="hq7z7m"
Accueil
Produits
Contact
```

---

# ❓ Questions d’analyse

1️⃣ Quel est le rôle du fichier **index.php** ?

2️⃣ Pourquoi utilise-t-on plusieurs **controllers** ?

3️⃣ Comment une page est-elle affichée dans une application MVC ?

4️⃣ Pourquoi cette organisation est utilisée dans les frameworks ?

---

# 🎓 Conclusion

Dans cette séance nous avons appris :

✔ comment naviguer entre plusieurs pages
✔ comment utiliser le fichier **index.php**
✔ comment appeler différents **controllers**
✔ comment organiser une petite application MVC

Ces notions permettent de comprendre **le fonctionnement interne des frameworks comme Symfony**.

---

* Controller
* Template
* Services

exactement comme dans Symfony.
