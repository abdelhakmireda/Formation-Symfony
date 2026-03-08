
---

# 📘 Séance 01 — Fonctionnement du Web et Bases de PHP

👨‍🏫 Responsable du module : **Reda Abdelhakmi**
📚 Module : **Introduction au Développement Web MVC**

---

# 🎯 Objectifs pédagogiques

À la fin de cette séance, l’étudiant sera capable de :

✔ comprendre comment fonctionne **le Web**

✔ comprendre l’architecture **Client / Serveur**

✔ comprendre le rôle du **serveur Web**

✔ comprendre le rôle du **langage PHP**

✔ écrire un **premier script PHP**

✔ utiliser **variables, conditions et boucles**

Cette séance pose **les bases nécessaires avant d’apprendre la Programmation Orientée Objet et MVC (Symfony / Laravel)**.

---

# 🌐 1 — Comment fonctionne le Web ?

Lorsque vous ouvrez un site web comme :

```
https://www.google.com
```

plusieurs éléments interviennent.

Un site web fonctionne grâce à **une communication entre un client et un serveur**.

---

# 🧭 Architecture Client / Serveur

Schéma simplifié :

```
Utilisateur
     │
     ▼
Navigateur (Chrome, Firefox)
     │
     │ requête HTTP
     ▼
Serveur Web (Apache / Nginx)
     │
     │ exécute
     ▼
Script PHP
     │
     │ génère
     ▼
HTML
     │
     ▼
Navigateur affiche la page
```

---

# 📌 Exemple réel

Quand un utilisateur tape dans le navigateur :

```
http://localhost/index.php
```

il se passe les étapes suivantes :

1️⃣ Le navigateur envoie une **requête HTTP**
2️⃣ Le serveur web reçoit la requête
3️⃣ Le serveur exécute le **script PHP**
4️⃣ PHP génère une page **HTML**
5️⃣ Le navigateur affiche la page

---

# 🧠 2 — Qu’est-ce que PHP ?

PHP signifie :

```
PHP: Hypertext Preprocessor
```

C’est un **langage de programmation côté serveur**.

Cela signifie que :

👉 le code PHP est exécuté **sur le serveur**
👉 le navigateur reçoit **seulement le résultat (HTML)**

---

# Exemple simple

Créer un fichier :

```
index.php
```

Code :

```php
<?php

echo "Bonjour les étudiants";

?>
```

Résultat dans le navigateur :

```
Bonjour les étudiants
```

---

# 🔹 3 — Les Variables en PHP

Les variables permettent de **stocker des informations**.

En PHP une variable commence toujours par :

```
$
```

---

## Exemple

```php
<?php

$nom = "Reda";
$age = 22;

echo $nom;

?>
```

Résultat :

```
Reda
```

---

# Types de données principaux

| Type    | Exemple         |
| ------- | --------------- |
| String  | `"Bonjour"`     |
| Integer | `10`            |
| Float   | `3.14`          |
| Boolean | `true`          |
| Array   | `["A","B","C"]` |

---

# 🔹 4 — Les Conditions

Les conditions permettent de **prendre une décision dans un programme**.

---

# 4.1 Condition `if / else`

Syntaxe :

```php
if (condition) {

    // code si vrai

} else {

    // code si faux

}
```

---

### Exemple

```php
<?php

$age = 20;

if ($age >= 18) {

    echo "Vous êtes majeur";

} else {

    echo "Vous êtes mineur";

}

?>
```

---

### Schéma logique

```
       condition
           │
     ┌─────┴─────┐
     │           │
   vrai        faux
     │           │
 exécuter      exécuter
 bloc IF      bloc ELSE
```

---

# 4.2 Condition sur une ligne — Opérateur Ternaire

PHP permet d'écrire une condition **sur une seule ligne**.

Syntaxe :

```php
condition ? valeur_si_vrai : valeur_si_faux;
```

---

### Exemple

```php
<?php

$age = 20;

echo ($age >= 18) ? "Majeur" : "Mineur";

?>
```

Résultat :

```
Majeur
```

---

### Exemple avec variable

```php
<?php

$note = 12;

$resultat = ($note >= 10) ? "Admis" : "Ajourné";

echo $resultat;

?>
```

---

# 🔹 4.3 Structure `switch / case`

La structure `switch` est utilisée lorsqu’on compare **une variable à plusieurs valeurs possibles**.

---

### Syntaxe

```php
switch(variable) {

    case valeur1:
        code;
        break;

    case valeur2:
        code;
        break;

    default:
        code;

}
```

---

### Exemple

```php
<?php

$jour = "lundi";

switch ($jour) {

    case "lundi":
        echo "Début de semaine";
        break;

    case "vendredi":
        echo "Fin de semaine";
        break;

    default:
        echo "Jour normal";

}

?>
```

---

# ⚖️ Différence entre `if` et `switch`

| IF                                | SWITCH                         |
| --------------------------------- | ------------------------------ |
| teste plusieurs conditions        | compare une variable           |
| plus flexible                     | plus lisible                   |
| utilisé pour conditions complexes | utilisé pour plusieurs valeurs |

---

# ⚡ Performance

Dans certains cas où l’on compare **une seule variable à plusieurs valeurs**, `switch` peut être **plus optimisé par PHP**.

Dans certaines situations :

```
switch peut être environ 5 à 10 fois plus rapide
```

Mais dans les applications modernes, la différence reste **souvent faible**.

On choisit donc généralement **la structure la plus lisible**.

---

# 🔹 5 — Les Boucles

Les boucles permettent de **répéter du code plusieurs fois**.

Elles sont très utiles pour :

* afficher des listes
* parcourir des tableaux
* traiter des données

---

# 5.1 Boucle `for`

Utilisée quand **on connaît le nombre d’itérations**.

---

### Exemple

```php
<?php

for ($i = 1; $i <= 5; $i++) {

    echo $i;
    echo "<br>";

}

?>
```

Résultat :

```
1
2
3
4
5
```

---

# 🔹 5.2 Boucle `foreach`

La boucle `foreach` est utilisée **pour parcourir un tableau**.

C’est la boucle **la plus utilisée dans le développement web**.

---

### Exemple

```php
<?php

$fruits = ["pomme", "banane", "orange"];

foreach ($fruits as $fruit) {

    echo $fruit;
    echo "<br>";

}

?>
```

Résultat :

```
pomme
banane
orange
```

---

### Explication

```php
foreach ($fruits as $fruit)
```

Signifie :

```
Pour chaque élément du tableau fruits
mettre cet élément dans la variable fruit
```

---

### Schéma logique

```
Tableau

[ pomme | banane | orange ]

        │
        ▼

Iteration 1 → fruit = pomme
Iteration 2 → fruit = banane
Iteration 3 → fruit = orange
```

---

# Foreach avec clé et valeur

```php
<?php

$etudiants = [
    "Alice" => 15,
    "Karim" => 12,
    "Sara" => 18
];

foreach ($etudiants as $nom => $note) {

    echo $nom . " : " . $note;
    echo "<br>";

}

?>
```

---

# 🧪 Exercices proposés

## Exercice 1 (facile)

Créer un fichier :

```
hello.php
```

Afficher :

```
Bonjour tout le monde
```

---

## Exercice 2

Créer un script affichant :

```
Nom : Sara
Age : 21
```

---

## Exercice 3

Créer une variable :

```php
$age = 17;
```

Afficher :

```
Majeur
ou
Mineur
```

---

## Exercice 4

Faire le même programme **avec l’opérateur ternaire**.

---

## Exercice 5

Créer un programme avec :

```php
$jour = "lundi";
```

Utiliser **switch case** pour afficher :

```
Début de semaine
```

---

## Exercice 6

Créer un tableau :

```
ordinateur
clavier
souris
écran
```

Afficher les éléments avec **foreach**.

---

# ⚖️ Questions d’analyse

1️⃣ Quelle est la différence entre **PHP et HTML** ?

2️⃣ Où est exécuté le code PHP ?

3️⃣ Quelle est la différence entre **if et switch** ?

4️⃣ Pourquoi utilise-t-on **foreach avec les tableaux** ?


---

# 🎓 Conclusion

Dans cette séance nous avons découvert :

✔ fonctionnement du **Web**
✔ architecture **client / serveur**
✔ bases du **langage PHP**
✔ variables
✔ conditions
✔ boucles
✔ tableaux

Ces bases sont **indispensables pour comprendre les frameworks modernes comme Symfony et Laravel**.

---

# 📚 Prochaine séance

Lors de la **Séance 02**, nous allons découvrir :

➡ **La Programmation Orientée Objet (OOP)**
➡ **Les classes et objets**
➡ **l’héritage et l’encapsulation**
➡ **les namespaces utilisés dans Symfony**

---
