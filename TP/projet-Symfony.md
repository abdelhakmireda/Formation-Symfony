## 🚀 Introduction

Ce guide vous explique comment mettre en place un projet Symfony permettant de gérer des étudiants et des cours. L'application inclut des fonctionnalités d'authentification, de vérification d'email et de réinitialisation de mot de passe. L'environnement de développement est simplifié grâce à Docker.

---

## 🛠️ Étape 1 : Configuration du projet Symfony

### Créer un nouveau projet Symfony

1. **Cloner le dépôt Docker pour Symfony**
   ```bash
   git clone https://github.com/abdelhakmireda/Environnement-D-veloppement-Docker-Symfony.git
   cd Environnement-D-veloppement-Docker-Symfony/
   ```

2. **Démarrer les conteneurs**
   ```bash
   docker-compose up -d
   ```

3. **Connecter les conteneurs au réseau Docker**
   ```bash
   docker network connect dev docker_mysql
   docker network connect dev docker_phpmyadmin
   docker network connect dev docker_www
   ```

4. **Accéder au conteneur Symfony**
   ```bash
   docker exec -it docker_www bash
   ```

5. **Créer un projet Symfony**
   ```bash
   symfony new myproject --version="6.4.*" --webapp
   cd myproject
   ```

6. **Démarrer le serveur Symfony**
   ```bash
   symfony serve -d
   ```

---

## 🏗️ Étape 2 : Configuration de Docker

Les étapes pour la configuration de Docker sont déjà intégrées dans l'environnement préconfiguré, comme indiqué dans la section **Configuration Docker** ci-dessus.

---

## 🔐 Étape 3 : Mise en place de l'authentification

1. **Installation du bundle de vérification d'email**
   ```bash
   composer require symfonycasts/verify-email-bundle
   ```

2. **Création du formulaire d'inscription**
   ```bash
   php bin/console make:registration-form
   ```

3. **Création du système d'authentification**
   ```bash
   php bin/console make:auth
   ```

4. **Création du système de réinitialisation de mot de passe**
   ```bash
   php bin/console make:reset-password
   ```

5. **Application des migrations**
   ```bash
   php bin/console make:migration
   php bin/console doctrine:migrations:migrate
   ```

---

## 📧 Étape 4 : Gestion des emails

1. **Installation des bundles nécessaires pour l'envoi d'emails**
   ```bash
   composer require symfony/mailer
   composer require symfony/brevo-mailer
   ```

2. **Configuration dans `.env`**
   ```ini
   MAILER_DSN=brevo+api://@default
   ```

---

## 📄 Pages Essentielles

### 🔑 Page de Connexion (Login)

```twig
{% extends 'base.html.twig' %}

{% block title %}Se Connecter{% endblock %}

{% block body %}
<main class="login-page">
    <section class="formulaire">
        <form method="post" class="signin-form">
            <div class="header">
                <div class="title-login">Se Connecter</div>
            </div>
            <div class="body flex">
                <label for="inputEmail" class="inputEmail">Email</label>
                <div class="input-icon">
                    <input type="email" value="{{ last_username }}" name="email" id="inputEmail" placeholder="Entrez votre adresse email" autocomplete="email" class="field" required autofocus>
                </div>
                <label for="inputPassword" class="inputPassword">Mot de passe</label>
                <div class="toggle-password-container">
                    <div class="input-icon">
                        <input type="password" name="password" id="inputPassword" placeholder="Entrez votre mot de passe" class="field" autocomplete="current-password" required {{ stimulus_controller('symfony/ux-toggle-password/toggle-password', { visibleLabel: '', hiddenLabel: '', buttonClasses: ['toggle-password-button'] }) }}>
                    </div>
                </div>
            </div>
            <div class="remember-password-container">
                <div class="remember-me-container">
                    <input type="checkbox" name="_remember_me" class="remember-me">
                    <div>Se rappeler du mot de passe</div>
                </div>
                <a href="{{ path('app_forgot_password_request') }}" class="link-login">Mot de passe oublié ?</a>
            </div>
            <button class="submit-btn" type="submit" formnovalidate>Se connecter</button>
            <div class="signin-login-switch-container">
                <span class="signin-login-switch-label">Vous n'avez pas de compte ?</span>
                <a href="{{ path('app_register') }}" class="link-login">S'enregistrer</a>
            </div>
            <input type="hidden" name="_csrf_token" value="{{ csrf_token('authenticate') }}"/>
            <span class="separator-label">Ou</span>
            <a href="" class="google-login-button">
                <span>Se connecter avec Google</span>
            </a>
        </form>
    </section>
</main>
{% endblock %}
```

### 📝 Page d'Inscription (Register)

```twig
{% extends 'base.html.twig' %}

{% block title %}S'enregistrer{% endblock %}

{% block body %}
<main class="login-page">
    <section class="formulaire">
        <div class="header">
            <div class="title-login">S'enregistrer</div>
        </div>
        {{ form_start(registrationForm) }}
        {{ form_errors(registrationForm) }}
        <div class="form-row">
            <div class="form-group">
                {{ form_label(registrationForm.nom, 'Nom', {'label_attr': {'class': 'label'}}) }}
                {{ form_widget(registrationForm.nom, {'attr': {'class': 'input-icon', 'placeholder': 'Entrez votre nom'}}) }}
            </div>
            <div class="form-group">
                {{ form_label(registrationForm.prenom, 'Prénom', {'label_attr': {'class': 'label'}}) }}
                {{ form_widget(registrationForm.prenom, {'attr': {'class': 'input-icon', 'placeholder': 'Entrez votre prénom'}}) }}
            </div>
        </div>
        <button type="submit" class="submit-btn">S'enregistrer</button>
        <div class="signin-login-switch-container">
            <span class="signin-login-switch-label">Vous avez déjà un compte ?</span>
            <a href="{{ path('app_login') }}" class="link-login">Se Connecter</a>
        </div>
        {{ form_end(registrationForm) }}
    </section>
</main>
{% endblock %}
```

### 🔄 Réinitialisation du Mot de Passe

#### 📨 Demande de Réinitialisation (request.html.twig)

```twig
{% extends 'base.html.twig' %}
{% block title %}Réinitialisation du mot de passe{% endblock %}
{% block body %}
<main class="login-page">
    <section class="formulaire">
        <form method="post" class="reset-password-request-form">
            {{ form_start(requestForm) }}
            <div class="header">
                <div class="title-login">Réinitialisation du mot de passe</div>
            </div>
            <div class="body flex">
                <div class="form-group">
                    {{ form_label(requestForm.email, 'Adresse email', {'label_attr': {'class': 'label'}}) }}
                    <div class="input-icon">
                        {{ form_widget(requestForm.email, {'attr': {'class': 'field', 'placeholder': 'Entrez votre adresse email'}}) }}
                    </div>
                </div>
                <div class="text-explanation">
                    <small>📧 Entrez votre adresse email et nous vous enverrons un lien pour réinitialiser votre mot de passe.</small>
                </div>
            </div>
            <button class="submit-btn" type="submit">Envoyer le lien de réinitialisation</button>
            <a href="{{ path('app_login') }}" class="link-login">Retour à la page de connexion</a>
            {{ form_end(requestForm) }}
        </form>
    </section>
</main>
{% endblock %}
```

#### 🔑 Réinitialisation du Mot de Passe (reset.html.twig)

```twig
{% extends 'base.html.twig' %}
{% block title %}Réinitialiser votre mot de passe{% endblock %}
{% block body %}
<main class="login-page">
    <section class="formulaire">
        <form method="post" class="reset-password-form">
            {{ form_start(resetForm) }}
            <div class="header">
                <div class="title-login">Réinitialiser votre mot de passe</div>
            </div>
            <div class="body flex">
                <div class="form-group">
                    {{ form_label(resetForm.plainPassword, 'Nouveau mot de passe', {'label_attr': {'class': 'label'}}) }}
                    <div class="input-icon">
                        {{ form_widget(resetForm.plainPassword, {'attr': {'

class': 'field', 'placeholder': 'Entrez votre nouveau mot de passe'}}) }}
                    </div>
                </div>
            </div>
            <button class="submit-btn" type="submit">Réinitialiser le mot de passe</button>
            {{ form_end(resetForm) }}
        </form>
    </section>
</main>
{% endblock %}
```
## Voici la structure des deux tables correspondantes à tes entités Symfony :

### Table `etudiqnt`
| Nom du champ     | Type                  | Contraintes                        |
|------------------|----------------------|------------------------------------|
| `id`            | `INT`                 | `PRIMARY KEY`, `AUTO_INCREMENT`   |
| `email`         | `VARCHAR(180)`        | `UNIQUE`, `NOT NULL`              |
| `roles`         | `JSON`                | `NOT NULL`                        |
| `password`      | `VARCHAR(255)`        | `NOT NULL`                        |
| `nom`           | `VARCHAR(255)`        | `NOT NULL`                        |
| `prenom`        | `VARCHAR(255)`        | `NOT NULL`                        |
| `date_naissance`| `DATETIME`            | `NOT NULL`                        |
| `created_at`    | `DATETIME`            | `NOT NULL`                        |
| `cour_id`       | `INT`                 | `FOREIGN KEY` vers `cour(id)`     |

### Table `cour`
| Nom du champ  | Type                 | Contraintes                        |
|--------------|---------------------|------------------------------------|
| `id`        | `INT`                | `PRIMARY KEY`, `AUTO_INCREMENT`   |
| `nom`       | `VARCHAR(255)`       | `NOT NULL`                        |
| `description`| `VARCHAR(255)`       | `NULLABLE`                        |
| `created_at` | `DATETIME`           | `NOT NULL`                        |

#### Relations :
- **Un étudiant (`etudiqnt`) appartient à un seul cours (`cour`).**
- **Un cours (`cour`) peut avoir plusieurs étudiants (`etudiqnt`).**

Cette structure reflète correctement la relation **ManyToOne** entre `Etudiqnt` et `Cour`.
---

## 📦 Conclusion

Ce guide vous montre comment configurer un projet Symfony avec Docker et intégrer une gestion d'authentification complète avec vérification d'email et réinitialisation de mot de passe. La structure est facilement extensible pour ajouter des fonctionnalités comme la gestion des étudiants et des cours, tout en permettant une mise en production rapide grâce à Docker.
