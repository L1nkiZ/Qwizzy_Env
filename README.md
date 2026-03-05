# Qwizzy - Documentation globale

## 📋 Table des matières

- [Vue d'ensemble](#vue-densemble)
- [Prérequis](#prérequis)
- [Structure des dépôts](#structure-des-dépôts)
- [Installation rapide](#installation-rapide)
- [Docker Compose disponibles](#docker-compose-disponibles)
- [Ports et accès aux services](#ports-et-accès-aux-services)
- [Credentials](#credentials)
- [Variables d'environnement](#variables-denvironnement)

---

## Vue d'ensemble

**Qwizzy** est une application de quiz composée de trois dépôts distincts :

| Dépôt | Description | Technologie |
|-------|-------------|-------------|
| `Qwizzy_API` | Backend REST & SOAP | Laravel 11, PHP 8.2, PostgreSQL 16 |
| `Qwizzy_Front` | Frontend | Nuxt 3 (Vue 3), pnpm |
| `Qwizzy_Env` | Orchestration Docker & documentation | Docker Compose |

Architecture : le frontend communique avec le backend via une **API REST et SOAP**. Le backend utilise un ORM (Eloquent) pour interagir avec la base de données PostgreSQL.

---

## Prérequis

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) ≥ 24
- [Git](https://git-scm.com/)

---

## Structure des dépôts

```
Qwizzy/
├── Qwizzy_API/      ← Backend Laravel
├── Qwizzy_Front/    ← Frontend Nuxt
└── Qwizzy_Env/      ← Ce dépôt (orchestration & docs)
```

Les trois dépôts doivent être clonés **dans le même dossier parent** pour que les chemins relatifs des Docker Compose fonctionnent.

---

## Installation rapide

### 1. Cloner les trois dépôts

```bash
git clone https://github.com/L1nkiZ/Qwizzy_API.git
git clone https://github.com/L1nkiZ/Qwizzy_Front.git
git clone https://github.com/L1nkiZ/Qwizzy_Env.git
```

### 2. Configurer le backend

```bash
cd Qwizzy_API
cp .env.example .env
```

> Le fichier `.env` est déjà configuré pour communiquer avec la base de données Docker. Aucune modification n'est nécessaire pour un démarrage local.

### 3. Choisir un profil Docker et démarrer

**Backend seul (API + BDD + pgAdmin) :**
```bash
cd Qwizzy_API
docker compose up -d
```

**Backend + monitoring (Prometheus + Grafana) :**
```bash
cd Qwizzy_API
docker compose -f docker-compose.monitoring.yml up -d
```

**Backend + Frontend :**
```bash
cd Qwizzy_Env
docker compose -f docker-compose.back-front.yml up -d
```

**Stack complète (tout) :**
```bash
cd Qwizzy_Env
docker compose -f docker-compose.yml up -d
```

---

## Docker Compose disponibles

### Dans `Qwizzy_API/`

| Fichier | Services inclus |
|---------|-----------------|
| `docker-compose.yml` | App Laravel · PostgreSQL · pgAdmin |
| `docker-compose.monitoring.yml` | App Laravel · PostgreSQL · Prometheus · Grafana |

### Dans `Qwizzy_Env/`

| Fichier | Services inclus |
|---------|-----------------|
| `docker-compose.back-front.yml` | App Laravel · PostgreSQL · Frontend Nuxt |
| `docker-compose.full.yml` | App Laravel · PostgreSQL · pgAdmin · Frontend Nuxt · Prometheus · Grafana |

---

## Ports et accès aux services

| Service | Port | URL |
|---------|------|-----|
| **API Laravel** | `8000` | http://localhost:8000 |
| **Swagger (doc API)** | `8000` | http://localhost:8000/api/documentation |
| **Métriques Prometheus** | `8000` | http://localhost:8000/api/metrics |
| **Frontend Nuxt** | `3000` | http://localhost:3000 |
| **pgAdmin** | `8080` | http://localhost:8080 |
| **PostgreSQL** | `5432` | `localhost:5432` (connexion directe) |
| **Prometheus** | `9090` | http://localhost:9090 |
| **Grafana** | `4000` | http://localhost:4000 |

---

## Credentials

| Service | Identifiant | Mot de passe |
|---------|-------------|--------------|
| **pgAdmin** | `admin@qwizzy.com` | `admin` |
| **PostgreSQL** | `qwizzy_user` | `qwizzy_password` |
| **Grafana** | `admin` | `admin` |
| **Base de données** | — | Database : `qwizzy_api` |

> Pour plus de détails, référez-vous au fichier README du dépôt en question