# SmartTask — AI-Ready Task & Project Management Platform

> **English:** Full-stack project & task management platform (Angular + Spring
> Boot), built step by step as a learning project. Teams create projects, add
> tasks (status, priority, due date), assign them to members, comment, attach
> files, get notified, and track progress on a dashboard — all behind JWT
> authentication with role-based permissions. See [`docs/`](docs/) (currently
> in French) for the full architecture, data model and API contract.

Application web full-stack de gestion de projets et de tâches, construite pas à pas
pour apprendre **Angular** (frontend) et **Spring Boot** (backend).

> Projet pédagogique : chaque étape est documentée dans [`docs/`](docs/) avant d'être codée.

---

## 1. En deux phrases

SmartTask permet à une équipe de créer des **projets**, d'y ajouter des **tâches**
(statut, priorité, échéance), de les **assigner** à des membres, de **commenter**,
de joindre des **fichiers**, de recevoir des **notifications** et de suivre
l'avancement sur un **dashboard**. L'accès est protégé par une
**authentification JWT** avec **rôles et permissions**.

## 2. Stack technique

| Couche | Technologie | Version visée |
|---|---|---|
| Frontend | Angular (standalone components + signals) | 21.x |
| Backend | Spring Boot (Web, Data JPA, Security, Validation) | 4.1.1 |
| Langage backend | Java | 17 |
| Base de données | PostgreSQL | 16 |
| Migrations SQL | Flyway | fourni par Spring Boot |
| Documentation API | OpenAPI / Swagger UI (springdoc) | 2.x |
| Tests backend | JUnit 5, Mockito, Testcontainers | — |
| Tests frontend | Karma/Jasmine (défaut Angular) | — |
| Conteneurisation | Docker + Docker Compose | 28.x / v2 |
| Build backend | Maven (via le *wrapper* `mvnw`) | 3.9.x |

## 3. Documentation (à lire dans cet ordre)

| Fichier | Contenu |
|---|---|
| [`docs/00-INSTALLATIONS.md`](docs/00-INSTALLATIONS.md) | Prérequis et configuration de l'environnement de développement |
| [`docs/01-ARCHITECTURE.md`](docs/01-ARCHITECTURE.md) | Architecture globale, découpage en couches, arborescence des dossiers |
| [`docs/02-MODELE-DONNEES.md`](docs/02-MODELE-DONNEES.md) | Entités, relations, diagramme ER, règles métier |
| [`docs/03-API-REST.md`](docs/03-API-REST.md) | Contrat d'API : tous les endpoints, formats JSON, codes d'erreur |
| [`docs/04-ROADMAP.md`](docs/04-ROADMAP.md) | Les 14 étapes du projet, de zéro au déploiement |
| [`docs/adr/0001-choix-techniques.md`](docs/adr/0001-choix-techniques.md) | **Pourquoi** ces technologies et pas d'autres |

## 4. Démarrage rapide

```powershell
# 1. Vérifier que l'environnement est complet
.\scripts\check-env.ps1

# 2. Démarrer la base de données (Docker Desktop doit être lancé)
docker compose up -d

# 3. Backend  (disponible à partir de l'étape 2)
cd backend
.\mvnw spring-boot:run          # -> http://localhost:8080

# 4. Frontend (disponible à partir de l'étape 3)
cd frontend
npm start                       # -> http://localhost:4200
```

| Service | URL | Identifiants |
|---|---|---|
| Frontend Angular | http://localhost:4200 | — |
| API backend | http://localhost:8080/api | — |
| Swagger UI | http://localhost:8080/swagger-ui.html | — |
| PostgreSQL (Docker) | `localhost:5433` | `smarttask` / `smarttask` |
| pgAdmin | http://localhost:5050 | `admin@smarttask.local` / `admin` |

> ℹ️ PostgreSQL est exposé sur le port **5433** (et non 5432) pour éviter tout conflit
> avec une installation PostgreSQL locale. Voir `docs/00-INSTALLATIONS.md`.

## 5. Arborescence

```
smarttask/
├── backend/            # API REST Spring Boot          (étape 2)
├── frontend/           # SPA Angular                   (étape 3)
├── docs/               # Documentation du projet
├── scripts/            # Scripts utilitaires
├── docker-compose.yml  # PostgreSQL + pgAdmin pour le dev
├── .env.example        # Modèle de variables d'environnement
└── README.md
```

## 6. Avancement

- [x] **Étapes 1–4** — Architecture, squelettes backend/frontend, authentification JWT
- [x] **Étapes 5–6** — Rôles & permissions, CRUD projets et membres
- [x] **Étapes 7–8** — CRUD tâches, kanban, recherche, filtres, tri, pagination
- [x] **Étapes 9–10** — Commentaires, notifications événementielles, fichiers joints
- [x] **Étapes 11–12** — Dashboard & statistiques, tests (unitaires, web-slice, intégration Testcontainers)
- [ ] **Étape 13** — Conteneurisation complète & déploiement
- [ ] **Étape 14** — Module IA

Détail des étapes : [`docs/04-ROADMAP.md`](docs/04-ROADMAP.md).

---

## Licence

Projet personnel d'apprentissage.
