# 00 — Environnement de développement

> Ce document liste les outils nécessaires pour développer et lancer SmartTask,
> ainsi que la configuration attendue. Plateforme de référence : **Windows 10/11
> (x64)**, shell **PowerShell** (les commandes s'adaptent facilement à Linux/macOS).

---

## 1. Prérequis

| Outil | Rôle dans le projet | Version minimale |
|---|---|---|
| **JDK (Java)** | Compiler et exécuter le backend Spring Boot | 17 |
| **Node.js** + **npm** | Outils Angular (CLI, serveur de dev) | Node 20.19+, 22.12+ ou 24.x |
| **Angular CLI** | Générer et builder le frontend | 22.x |
| **Docker Desktop** | PostgreSQL et pgAdmin en conteneurs | 28.x + Compose v2 |
| **Git** | Gestion de versions | 2.4x |
| **Maven** | Build backend | *non requis* — fourni par le wrapper `mvnw` |

---

## 2. Java (JDK 17)

Spring Boot 4.1 exige **Java 17 minimum**. La variable `JAVA_HOME` doit pointer
vers le JDK :

```powershell
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\Program Files\Java\jdk-17", "User")
```

Après avoir rouvert le terminal :

```powershell
java -version
javac -version    # doit répondre : un JDK est requis, pas seulement un JRE
```

---

## 3. Angular CLI

```powershell
npm install -g @angular/cli
ng version
```

---

## 4. Maven via le wrapper

Le projet embarque le *Maven Wrapper* : aucune installation globale n'est
nécessaire. Dans `backend/` :

```powershell
.\mvnw clean install        # compiler + tester + packager
.\mvnw spring-boot:run      # lancer l'application
.\mvnw test                 # lancer uniquement les tests
```

---

## 5. PostgreSQL (Docker)

La base tourne dans Docker, exposée sur le port **5433** pour éviter tout conflit
avec une éventuelle installation PostgreSQL locale (port 5432).

```powershell
docker compose up -d              # démarrer PostgreSQL + pgAdmin
docker compose ps                 # les conteneurs doivent être "running"/"healthy"
```

Connexion : `localhost:5433`, base `smarttask`, utilisateur `smarttask`
(valeurs de développement, définies dans `.env.example`).

pgAdmin est disponible sur http://localhost:5050. Pour y enregistrer le serveur,
utiliser comme *Host* `postgres` (nom du service Docker) et le port `5432` :
pgAdmin s'exécute dans le même réseau Docker.

```powershell
docker compose stop         # arrêter (données conservées)
docker compose down         # supprimer les conteneurs (données conservées)
docker compose down -v      # tout supprimer, y compris les données
```

---

## 6. Vérification de l'environnement

Le script `scripts/check-env.ps1` contrôle les outils, leurs versions et la
variable `JAVA_HOME` :

```powershell
.\scripts\check-env.ps1
```

Si PowerShell bloque l'exécution de scripts :

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

---

## 7. Ports utilisés

| Port | Service |
|---|---|
| `4200` | Serveur de dev Angular |
| `8080` | API Spring Boot |
| `5433` | PostgreSQL (Docker) |
| `5050` | pgAdmin |
