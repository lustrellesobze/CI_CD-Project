# Configuration du projet Laravel

## État actuel

Le projet Laravel **Laravel 12** a été créé avec succès. La structure de base est en place.

## Problème rencontré : Dépendances non installées

L'installation des dépendances Composer a rencontré des difficultés liées à :
- **Erreur SSL** : "unable to get local issuer certificate"
- **Timeouts réseau** : connexion à GitHub lente ou bloquée

## Modifications effectuées

1. **php.ini** (WAMP) : Configuration des certificats SSL
   - Fichier : `C:\wamp64\bin\php\php-8.4.17\php.ini`
   - `curl.cainfo` et `openssl.cafile` pointent vers le certificat CA de phpMyAdmin

2. **Composer** : Configuration globale du certificat CA
   - `composer config -g cafile "C:\wamp64\apps\phpmyadmin5.2.0\vendor\composer\ca-bundle\res\cacert.pem"`

## Étapes pour terminer l'installation

### 1. Redémarrer WAMP (pour appliquer les changements php.ini)
Cliquez sur l'icône WAMP → Redémarrer tous les services

### 2. Installer les dépendances
Ouvrez un terminal dans le dossier du projet et exécutez :

```bash
cd c:\Users\USER\Desktop\Laravel_CI_CD
composer install
```

### 3. Si les erreurs SSL persistent
Téléchargez manuellement `cacert.pem` depuis https://curl.se/ca/cacert.pem et placez-le dans `C:\wamp64\bin\php\php-8.4.17\extras\ssl\`, puis mettez à jour php.ini avec ce chemin.

### 4. Générer la clé d'application
```bash
php artisan key:generate
```

### 5. Créer la base de données SQLite
```bash
# Le fichier database.sqlite sera créé automatiquement
php artisan migrate
```

### 6. Lancer le serveur de développement
```bash
php artisan serve
```

Puis ouvrez http://127.0.0.1:8000 dans votre navigateur.

## Structure du projet

```
Laravel_CI_CD/
├── app/           # Logique applicative
├── config/        # Configuration
├── database/      # Migrations et seeders
├── public/        # Point d'entrée web
├── resources/     # Vues, CSS, JS
├── routes/        # Définition des routes
└── ...
```

## Connexion MySQL (optionnel)

Pour utiliser MySQL au lieu de SQLite, modifiez le fichier `.env` :

```
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_ci_cd
DB_USERNAME=root
DB_PASSWORD=
```

Puis créez la base de données dans phpMyAdmin et exécutez `php artisan migrate`.
