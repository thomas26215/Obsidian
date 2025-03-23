## Introduction

La sécurité dans Symfony repose sur deux étapes principales :

1. **L'authentification** : Identification de l'utilisateur.
2. **L'autorisation** : Détermination des droits d'accès aux ressources.

Symfony propose un système de pare-feu pour protéger les URL et déclencher le processus d'authentification.

---

## 1. Pare-Feu : Authentification

Le pare-feu est chargé de protéger l'application en filtrant les requêtes HTTP selon des patterns d'URL.

### Fonctionnement :

- Définition dans `security.yaml`.
- Permet de restreindre l'accès à certaines parties du site.
- Active un mécanisme d'authentification si nécessaire.

Exemple :

```yaml
firewalls:
    main:
        pattern: ^/
        provider: app_user_provider
        form_login:
            login_path: app_login
            check_path: app_login
            enable_csrf: true
        logout:
            path: app_logout
            target: home
```

---

## 2. Contrôle d'Accès : Autorisation

Une fois authentifié, l'utilisateur doit posséder les autorisations pour accéder aux ressources demandées.

### Fonctionnement :

- L'accès est contrôlé via `access_control` ou des annotations.
- Si l'utilisateur n'est pas autorisé, il reçoit une erreur HTTP 403.

Exemple :

```yaml
access_control:
    - { path: ^/admin, roles: ROLE_ADMIN }
    - { path: ^/usager, roles: ROLE_CLIENT }
```

Avec annotations :

```php
#[IsGranted('ROLE_ADMIN')]
public function adminDashboard(): Response {
    // Accessible uniquement aux administrateurs
}
```

---

## 3. Configuration de la Sécurité dans `security.yaml`

Symfony facilite la configuration de la sécurité via un fichier unique `security.yaml`.

### Sections principales :

- **`providers`** : Définit la source des utilisateurs.
- **`role_hierarchy`** : Gère les hiérarchies de rôles.
- **`password_hashers`** : Définit l'encodage des mots de passe.
- **`firewalls`** : Liste les pare-feux et leurs paramètres.
- **`access_control`** : Liste les règles d'accès par URL.

Exemple :

```yaml
providers:
    app_user_provider:
        entity:
            class: App\Entity\Usager
            property: email
role_hierarchy:
    ROLE_ADMIN: ROLE_CLIENT
password_hashers:
    Symfony\Component\Security\Core\User\PasswordAuthenticatedUserInterface: 'auto'
```

---

## 4. Mise en Place de l'Authentification

Symfony permet de générer automatiquement une authentification via un formulaire.

### Commande :

```bash
php bin/console make:security:form-login
```

Elle génère :

- Un **contrôleur** : `SecurityController.php`
- Un **template Twig** : `login.html.twig`
- Une mise à jour de `security.yaml`

### Adaptation de `SecurityController.php`

Si l'application gère plusieurs langues :

```php
#[Route(
    path: '/{_locale}/login',
    name: 'app_login',
    requirements: ['_locale' => '%app.supported_locales%']
)]
public function login(AuthenticationUtils $authenticationUtils): Response {
    // ...
}
```

---

## 5. Adapter le Formulaire d'Authentification

Le formulaire doit contenir un token CSRF pour la sécurité.

Exemple de `login.html.twig` :

```twig
<form method="post">
    {% if error %}
        <div class="alert alert-danger">{{ error.messageKey|trans(error.messageData, 'security') }}</div>
    {% endif %}
    <label for="username">Email</label>
    <input type="email" name="_username" id="username" required autofocus>
    <label for="password">Mot de Passe</label>
    <input type="password" name="_password" id="password" required>
    <input type="hidden" name="_csrf_token" value="{{ csrf_token('authenticate') }}">
    <button type="submit">Connexion</button>
</form>
```

---

## 6. Gestion des Utilisateurs et des Rôles

Dans un contrôleur, on peut :

- Récupérer l'utilisateur authentifié :

```php
$user = $this->getUser();
```

- Tester son rôle :

```php
if (!$this->isGranted('ROLE_ADMIN')) {
    throw $this->createAccessDeniedException();
}
```

- En Twig :

```twig
{% if is_granted('ROLE_ADMIN') %}
    <a href="...">Gérer</a>
{% endif %}
```
