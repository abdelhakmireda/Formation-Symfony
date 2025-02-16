
# 🚀 Symfony 6.4 - Doctrine, Formulaires, Gestion des Erreurs et API  

## 1. Doctrine : Gestion des Entités et Requêtes  

### 1.1 **Le Rôle du Repository et de l’EntityManager**  

- **EntityManager** : Il est utilisé pour interagir avec la base de données (insertion, mise à jour, suppression, etc.).
- **Repository** : Il permet de récupérer des objets depuis la base de données avec des requêtes spécifiques.

**Exemple : Utilisation du Repository pour récupérer des données**  
```php
$article = $this->getDoctrine()->getRepository(Article::class)->find(1);
```
- Ici, on récupère l'article avec l'ID `1`.

**Exemple : Utilisation de EntityManager pour insérer des données**  
```php
$entityManager = $this->getDoctrine()->getManager();
$article = new Article();
$article->setTitle("Symfony est génial !");
$entityManager->persist($article); // Prépare l'insertion
$entityManager->flush(); // Exécute l'insertion dans la base
```
- `persist($article)` : Prépare l’objet pour l’ajouter en base de données.
- `flush()` : Exécute réellement l’insertion.

---

## 2. Commandes Symfony pour les Formulaires  

Pour générer un formulaire automatiquement, utilisez :  
```bash
php bin/console make:form
```
Il vous demandera le nom du formulaire et l’entité associée.  


## 3. Les Types de Formulaires et leurs Widgets  

Symfony propose plusieurs types de champs que l'on peut utiliser avec les formulaires.  

### 3.1 **Les Types de Champs les Plus Utilisés**
| Type de Champ        | Utilisation |
|----------------------|-------------|
| `TextType`          | Champ texte classique |
| `TextareaType`      | Zone de texte multi-lignes |
| `EmailType`         | Champ email |
| `PasswordType`      | Mot de passe |
| `IntegerType`       | Nombre entier |
| `ChoiceType`        | Liste déroulante |
| `CheckboxType`      | Case à cocher |
| `DateType`          | Sélecteur de date |
| `FileType`          | Champ de fichier |

**Exemple : Création d'un formulaire avec différents types de champs**
```php
use Symfony\Component\Form\Extension\Core\Type\TextType;
use Symfony\Component\Form\Extension\Core\Type\TextareaType;
use Symfony\Component\Form\Extension\Core\Type\EmailType;
use Symfony\Component\Form\Extension\Core\Type\SubmitType;
use Symfony\Component\Form\AbstractType;
use Symfony\Component\Form\FormBuilderInterface;
use Symfony\Component\OptionsResolver\OptionsResolver;
use App\Entity\Article;

class ArticleType extends AbstractType
{
    public function buildForm(FormBuilderInterface $builder, array $options)
    {
        $builder
            ->add('title', TextType::class, [
                'label' => 'Titre de l\'article',
                'required' => true,
            ])
            ->add('content', TextareaType::class, [
                'label' => 'Contenu',
                'attr' => ['rows' => 5]
            ])
            ->add('email', EmailType::class, [
                'label' => 'Email de l\'auteur'
            ])
            ->add('save', SubmitType::class, [
                'label' => 'Publier'
            ]);
    }

    public function configureOptions(OptionsResolver $resolver)
    {
        $resolver->setDefaults([
            'data_class' => Article::class,
        ]);
    }
}
```

## 4. Affichage du Formulaire en Twig  

### 4.1 **Méthode Rapide avec `form()`**
```twig
{{ form(form) }}
```
- Génère automatiquement l’ensemble du formulaire.

### 4.2 **Méthode Personnalisée avec `form_widget()`**
```twig
{{ form_start(form) }}
    {{ form_widget(form.title) }}
    {{ form_widget(form.content) }}
    <button type="submit">Envoyer</button>
{{ form_end(form) }}
```
- `form_start(form)`: Démarre le formulaire.
- `form_widget(form.title)`: Affiche le champ spécifique.
- `form_end(form)`: Ferme le formulaire.

---

## 5. **Gestion des Messages Flash**  

### 5.1 **Ajout d’un Message Flash dans le Contrôleur**
```php
$this->addFlash('success', 'Votre article a été enregistré avec succès !');
```
### 5.2 **Affichage des Messages Flash en Twig**
```twig
{% for message in app.flashes('success') %}
    <div class="alert alert-success">{{ message }}</div>
{% endfor %}
```
- Les messages flash sont stockés temporairement en session et disparaissent après affichage.

---

## 6. **Gestion des Erreurs dans un Formulaire**  

### 6.1 **Afficher les Erreurs de Validation**
```twig
{{ form_errors(form) }}
```
- Affiche les erreurs globales.

### 6.2 **Afficher les Erreurs pour un Champ Spécifique**
```twig
{{ form_errors(form.title) }}
```
- Affiche les erreurs uniquement pour `title`.


## 7. **Les Services dans Symfony**  

Un **service** est une classe PHP qui effectue une tâche précise (ex: envoi d’email, traitement d’images, etc.).

### 7.1 **Création d’un Service**
Créez un fichier `src/Service/MonService.php` :
```php
namespace App\Service;

class MonService {
    public function direBonjour() {
        return "Bonjour, bienvenue sur notre site !";
    }
}
```
### 7.2 **Utilisation d’un Service dans un Contrôleur**
```php
use App\Service\MonService;

public function index(MonService $monService)
{
    $message = $monService->direBonjour();
    return $this->render('home.html.twig', [
        'message' => $message
    ]);
}
```
### 7.3 **Affichage en Twig**
```twig
<p>{{ message }}</p>
```

---

## 8. **Introduction aux API avec Symfony**  

### 8.1 **Installation de API Platform**
```bash
composer require api
```

### 8.2 **Exposition d’une Entité en API**
Ajoutez l’annotation `#[ApiResource]` dans `Article.php` :
```php
use ApiPlatform\Metadata\ApiResource;
#[ApiResource]
class Article { ... }
```
Ensuite, accédez aux données via :  
```
http://127.0.0.1:8000/api/articles
```

---

# 🎯 **Résumé**
✅ **Doctrine** : `EntityManager` permet la gestion des entités, `Repository` permet les requêtes.  
✅ **Formulaires** : Création avec `make:form`, affichage avec `form_widget()`.  
✅ **Validation & Flash** : `persist()` ajoute un objet, `flush()` enregistre dans la base, `addFlash()` affiche un message temporaire.  
✅ **Services** : Utilisation d’un service pour modulariser le code.  
✅ **API Platform** : Facile à mettre en place avec `#[ApiResource]`.  

Besoin d’un approfondissement sur un point en particulier ? 🚀
