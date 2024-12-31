
# GestionUtilisateursLaravel

# Documentation de Projet Web - Application de Gestion des Utilisateurs

## 1. Introduction

**Objectif du projet :**  
Développer une application web de gestion des utilisateurs, permettant l'inscription, la connexion, et l'administration des profils. L'objectif est de créer un système robuste et sécurisé, facilitant la gestion des utilisateurs via une interface intuitive.  

**Contexte :**  
Ce projet s'inscrit dans le cadre d'un exercice académique visant à approfondir la maîtrise du framework Laravel. Il simule un cas concret de développement d'une application web utilisée pour gérer les utilisateurs d'une plateforme.  

**Fonctionnalités principales :**  
- Authentification des utilisateurs (connexion/inscription)  
- Gestion des profils (CRUD)  
- Tableau de bord personnalisé  
- API REST pour la gestion des utilisateurs  
- Notifications en temps réel  

---

## 2. Conception

### Diagramme de cas d'utilisation
![Diagramme de cas d'utilisation](./diagrams/use_case.png)

### Diagramme de classes
![Diagramme de classes](./diagrams/class_diagram.png)

### Diagramme de séquence
![Diagramme de séquence](./diagrams/sequence_diagram.png)

---

## 3. Technologies utilisées

**Framework principal :** Laravel  
**Langage :** PHP  
**Base de données :** MySQL  
**Front-end :** Vue.js  
**Outils de versioning :** Git, GitHub  
**Serveur :** Docker (Apache, PHP, MySQL)  
**Gestion des dépendances :** Composer et NPM  

---

## 4. Architecture de l'application

**Modèles (Models) :**  
- User : Représentation des utilisateurs  
- Profile : Informations supplémentaires des utilisateurs  

**Vues (Views) :**  
- Pages Blade pour l'authentification, le tableau de bord et la gestion des profils  

**Contrôleurs (Controllers) :**  
- AuthController : Gestion de l'authentification  
- UserController : CRUD des utilisateurs  

**Routes :**  
- web.php : Routes pour les vues utilisateurs  
- api.php : Routes pour l'API REST  

**Middleware :**  
- Vérification des utilisateurs authentifiés  
- Protection CSRF et gestion des permissions  

---

## 5. Avancement

**Fonctionnalités développées :**  
- [x] Authentification (inscription, connexion, déconnexion)  
- [x] Gestion des profils utilisateurs  
- [x] API REST pour l'administration des utilisateurs  
- [ ] Notifications en temps réel (en cours)  

---

## 6. Mise en œuvre

### Déploiement avec Docker

**Fichier docker-compose.yml :**
```yaml
version: '3.8'
services:
  app:
    build: 
      context: .
      dockerfile: Dockerfile
    container_name: laravel_app
    restart: unless-stopped
    working_dir: /var/www
    volumes:
      - ./:/var/www
    ports:
      - "8000:8000"
    depends_on:
      - db
  db:
    image: mysql:8.0
    container_name: mysql_db
    restart: unless-stopped
    environment:
      MYSQL_DATABASE: gestion
      MYSQL_USER: user
      MYSQL_PASSWORD: password
      MYSQL_ROOT_PASSWORD: root
    ports:
      - "3306:3306"
    volumes:
      - dbdata:/var/lib/mysql
volumes:
  dbdata:
```

**Fichier Dockerfile :**
```dockerfile
FROM php:8.1-fpm

WORKDIR /var/www

RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    curl \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

RUN curl -sS https://getcomposer.org/installer | php -- \
    && mv composer.phar /usr/local/bin/composer

COPY . .

RUN composer install

CMD ["php", "artisan", "serve", "--host=0.0.0.0"]

EXPOSE 8000
```

---

### Captures d'écran
![Page de connexion](./screenshots/login.png)  
![Tableau de bord](./screenshots/dashboard.png)  

### Code source
Téléchargez le code source compressé : [app_code.zip](./downloads/app_code.zip)  

---

## 7. Difficultés rencontrées

- **Problème :** Intégration de Docker avec Laravel.  
  **Solution :** Création de Dockerfile et docker-compose.yml avec gestion des volumes persistants.  
- **Problème :** Communication entre conteneurs.  
  **Solution :** Utilisation de Docker Networks pour une communication fluide entre les services.  

---

## 8. Conclusion

**Résumé de l'expérience :**  
Le projet a permis de mettre en place une architecture conteneurisée avec Docker, simplifiant le déploiement et garantissant la portabilité de l'application.  

**Axes d'amélioration :**  
- Finalisation des notifications en temps réel  
- Ajout de tests unitaires et fonctionnels  
- Optimisation des performances générales et amélioration des requêtes SQL  

---

