# Plane — Gestion de projet open source

## Qu'est-ce que c'est

Plane est une plateforme de **gestion de projet open source** : issues (tickets), cycles (sprints), modules, roadmaps et documents, dans une interface moderne et rapide. C'est l'alternative souveraine aux outils de project management SaaS.

## Ce qu'il peut faire

- **Issues & tickets** : création rapide, priorités, labels, assignations, sous-tâches, relations entre tickets
- **Cycles (sprints)** : planification itérative avec burn-down et suivi de vélocité
- **Modules** : regroupement de tickets par fonctionnalité ou lot de travaux
- **Vues multiples** : liste, kanban, calendrier, feuille de calcul, Gantt (timeline)
- **Pages / docs** : documentation projet intégrée (notes de specs, comptes-rendus)
- **Espaces publics** : partage d'une roadmap ou d'un board en lecture seule (module Space)
- **API REST + webhooks** : automatisation complète depuis n8n (création de tickets, transitions…)
- **Multi-projets et multi-équipes** : workspaces, membres, rôles

## Ce qu'il remplace

| Logiciel remplacé | Type |
|---|---|
| **Jira (Atlassian)** | Gestion de projet / tickets |
| **Linear** | Issue tracking produit |
| **Asana** | Gestion de tâches d'équipe |
| **Monday.com** | Work management |
| **Trello (usages avancés)** | Kanban |

## Cas d'usage pour Fluxcaler

- Piloter vos projets clients et internes avec sprints et roadmap, données hébergées chez vous
- Créer automatiquement des tickets depuis n8n (emails, formulaires, alertes monitoring)
- Publier une roadmap publique pour vos clients (Plane Space)

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `PLANE_WEB_URL` | URL publique de l'instance | http://localhost:8087 |
| `PLANE_SECRET_KEY` | Clé secrète Django | (générée) |
| `PLANE_DB_PASSWORD` | Mot de passe PostgreSQL dédié | (généré) |
| `PLANE_RABBITMQ_PASSWORD` | Mot de passe RabbitMQ | (généré) |
| `PLANE_MINIO_PASSWORD` | Mot de passe MinIO (stockage fichiers) | (généré) |

Le compte administrateur se crée **au premier accès** via `/god-mode/` (instance admin) puis « Sign up » sur l'interface principale.

## Ports

| Port | Usage |
|------|-------|
| 8087 | Interface web Plane (proxy intégré : web, space, admin, api) |

## Architecture

Stack complète : proxy nginx, frontend web, space (partage public), admin, API Django, worker + beat (tâches asynchrones), PostgreSQL 15, Valkey (Redis), RabbitMQ, MinIO (stockage S3 local).

## Ressources

- [Documentation officielle](https://docs.plane.so/)
- [GitHub](https://github.com/makeplane/plane)
