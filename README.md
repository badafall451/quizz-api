<<<<<<< HEAD
# 🎓 Quiz App - Application Web de Quiz en Ligne

[![Laravel](https://img.shields.io/badge/Laravel-12.x-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)](https://laravel.com)
[![React](https://img.shields.io/badge/React-19.x-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-3.x-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)](https://tailwindcss.com)
[![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com)
[![Docker](https://img.shields.io/badge/Docker-Compose-2496ED?style=for-the-badge&logo=docker&logoColor=white)](https://www.docker.com)

Une plateforme dynamique et moderne de quiz en ligne développée avec une architecture découplée **Laravel 12 (API REST)** et **React 19 (SPA)**. Ce projet permet aux utilisateurs d'évaluer leurs connaissances à travers des séries de questions à choix multiples, de suivre leur progression, de consulter un classement global et offre aux administrateurs une interface complète de gestion des contenus.

---

## 📌 Sommaire

- [Fonctionnalités](#-fonctionnalités)
  - [Côté Utilisateur / Joueur](#côté-utilisateur--joueur)
  - [Côté Administrateur](#côté-administrateur)
- [Technologies Utilisées](#-technologies-utilisées)
- [Architecture du Projet](#-architecture-du-projet)
- [Prérequis](#-prérequis)
- [Installation et Démarrage](#-installation-et-démarrage)
  - [Option 1 : Démarrage Rapide avec Docker Compose (Recommandé)](#option-1--démarrage-rapide-avec-docker-compose-recommandé)
  - [Option 2 : Installation Manuelle (Développement Local)](#option-2--installation-manuelle-développement-local)
- [Endpoints API Principaux](#-endpoints-api-principaux)
- [Auteur](#-auteur)

---

## 🚀 Fonctionnalités

### 👤 Côté Utilisateur / Joueur

- **Authentification Sécurisée** : Inscription et connexion basées sur Laravel Sanctum (tokens d'API).
- **Catalogue de Quiz** : Exploration par catégories, niveaux de difficulté et recherche par mots-clés.
- **Session de Quiz Interactive** :
  - Minuteur dynamique / Chronomètre par quiz.
  - Progression en temps réel avec navigation fluide entre les questions.
  - Sauvegarde et évaluation instantanée des réponses.
- **Résultats Détaillés** : Affichage du score (pourcentage), nombre de bonnes/mauvaises réponses, temps écoulé et explications des réponses.
- **Historique Personnalisé** : Consultation des tentatives passées et suivi de la progression.
- **Leaderboard (Classement Général)** : Tableau d'honneur des meilleurs joueurs et scores cumulés.

### 🛡️ Côté Administrateur

- **Tableau de Bord Analytics** : Métriques globales (nombre d'utilisateurs, quiz créés, questions enregistrées, participations totales).
- **Gestion des Quiz (CRUD)** : Création, modification, catégorisation et suppression de quiz.
- **Gestion des Questions (CRUD)** : Ajout de questions à choix multiples, définition de la bonne réponse, points accordés et explications pédagogiques.

---

## 🛠️ Technologies Utilisées

| Layer | Technologie | Description |
| :--- | :--- | :--- |
| **Backend API** | **Laravel 12** | Framework PHP pour l'API RESTful et l'authentification Sanctum |
| **Frontend SPA** | **React 19** | Bibliothèque UI avec React Router v7 |
| **Styling & UI** | **Tailwind CSS** + **Framer Motion** | Interface moderne, responsive et animations fluides |
| **Icons & Toasts** | **Lucide React** & **React Hot Toast** | Retours utilisateurs et typographie visuelle |
| **Base de Données**| **MySQL 8** | Stockage persistant des données (Quiz, Questions, Utilisateurs, Résultats) |
| **Containerization**| **Docker & Docker Compose** | Orchestration multi-conteneurs (App, Nginx, Frontend, DB) |

---

## 📁 Architecture du Projet

```text
laravel-react/
├── docker-compose.yml         # Fichier d'orchestration Docker Compose
├── backend/                   # API RESTful Laravel 12
│   ├── app/
│   │   ├── Http/Controllers/  # AuthController, QuizController, QuestionController, ResultController
│   │   └── Models/            # User, Quiz, Question, Option, Result
│   ├── database/
│   │   ├── migrations/        # Schema de la base de données
│   │   └── seeders/           # Données de démonstration
│   ├── routes/
│   │   └── api.php            # Définition des routes de l'API RESTful
│   └── Dockerfile             # Image Docker PHP-FPM
└── frontend/                  # Application Client React 19
    ├── src/
    │   ├── admin/             # Dashboard d'administration et formulaires CRUD
    │   ├── user/              # Interface Joueur (Quiz, Play, Leaderboard, History)
    │   ├── components/        # Composants réutilisables (Navbar, Cards, Modals)
    │   └── context/           # Context d'Authentification
    └── Dockerfile             # Image Docker React
```

---

## 📋 Prérequis

Pour exécuter ce projet sur votre machine, vous avez besoin de :

- **Git**
- **Docker Desktop** *(pour le lancement via Docker Compose)*
- **Ou** pour une exécution manuelle :
  - **PHP >= 8.2** & **Composer**
  - **Node.js >= 18** & **npm**
  - **MySQL >= 8.0**

---

## ⚙️ Installation et Démarrage

### Option 1 : Démarrage Rapide avec Docker Compose (Recommandé)

1. **Cloner le dépôt et se placer dans le projet** :
   ```bash
   git clone <URL_DU_DEPOT>
   cd laravel-react
   ```

2. **Lancer l'environnement avec Docker Compose** :
   ```bash
   docker-compose up -d --build
   ```

3. **Appliquer les migrations et les données initiales** :
   ```bash
   docker exec -it quiz-app php artisan migrate --seed
   ```

4. **Accéder aux services** :
   - **Frontend (React)** : [http://localhost:3000](http://localhost:3000)
   - **Backend (API Nginx)** : [http://localhost:8000](http://localhost:8000)

---

### Option 2 : Installation Manuelle (Développement Local)

#### 1. Backend (Laravel)

```bash
cd backend

# Installer les dépendances PHP
composer install

# Copier le fichier d'environnement
cp .env.example .env

# Générer la clé d'application Laravel
php artisan key:generate

# Configurer l'accès à la base de données MySQL dans le fichier .env
# (DB_DATABASE, DB_USERNAME, DB_PASSWORD)

# Lancer les migrations et les seeders
php artisan migrate --seed

# Démarrer le serveur API Laravel
php artisan serve --port=8000
```

#### 2. Frontend (React)

```bash
cd ../frontend

# Installer les packages Node
npm install

# Démarrer le serveur de développement React
npm start
```

Accédez ensuite à l'application via [http://localhost:3000](http://localhost:3000).

---

## 📡 Endpoints API Principaux

| Méthode | Endpoint | Description | Accès |
| :--- | :--- | :--- | :--- |
| `POST` | `/api/register` | Inscription d'un nouvel utilisateur | Public |
| `POST` | `/api/login` | Connexion et émission du token Sanctum | Public |
| `GET` | `/api/quizzes` | Liste des quiz disponibles | Public |
| `GET` | `/api/quizzes/categories` | Catégories de quiz disponibles | Public |
| `GET` | `/api/leaderboard` | Classement général des joueurs | Public |
| `GET` | `/api/quizzes/{quiz}/questions` | Charger les questions d'un quiz | Authentifié |
| `POST` | `/api/submit-quiz` | Soumettre une tentative et calculer le score | Authentifié |
| `GET` | `/api/results/me` | Historique des scores de l'utilisateur | Authentifié |
| `POST` | `/api/quizzes` | Créer un quiz | Admin |
| `PUT` | `/api/quizzes/{quiz}` | Modifier un quiz | Admin |
| `DELETE` | `/api/quizzes/{quiz}` | Supprimer un quiz | Admin |
| `POST` | `/api/questions` | Ajouter une question | Admin |
| `GET` | `/api/admin/stats` | Statistiques globales pour l'Admin | Admin |

---

## ✍️ Auteur

Développé par **Alioune Badara Fall**  
*Licence 3 - Projet d'Application Web (Laravel & React)*
=======

>>>>>>> 1caf6bae8bb6b9ab17152570aaeed79dd3f7e21b
