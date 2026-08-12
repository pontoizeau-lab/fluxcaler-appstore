# NocoBase — Plateforme no-code pour applications métier

## Qu'est-ce que c'est

NocoBase est une plateforme **no-code / low-code open source** qui permet de construire des applications métier (CRM, ERP léger, outils internes, bases de gestion) directement sur vos propres données, sans écrire de code. Toute la logique est organisée autour de **collections** (tables), de **blocs** d'interface (tableaux, formulaires, kanban, calendriers) et de **workflows** déclenchables.

## Ce qu'il peut faire

- **Construire des outils internes** : interfaces d'administration, suivis de commandes, gestion de stocks, annuaires
- **Modéliser vos données** : collections relationnelles avec champs calculés, relations 1-N / N-N, vues filtrées
- **Interfaces par glisser-déposer** : pages, menus, tableaux, formulaires, kanban, calendrier, graphiques
- **Workflows intégrés** : déclencheurs (création, modification, planification) et actions automatisées
- **Droits d'accès fins** : rôles et permissions par collection, champ et action
- **Plugins** : système extensible (auth, import/export, API REST automatique sur chaque collection)
- **API REST native** : chaque collection est exploitable depuis n8n via HTTP Request

## Ce qu'il remplace

| Logiciel remplacé | Type |
|---|---|
| **Airtable** | Base de données no-code |
| **Microsoft PowerApps** | Créateur d'apps internes |
| **Retool** | Outils internes low-code |
| **Salesforce (usages simples)** | CRM personnalisé |

## Cas d'usage pour Fluxcaler

- Construire un CRM ou un back-office sur mesure alimenté par vos workflows n8n
- Centraliser des données métier avec une interface propre pour les équipes
- Prototyper une application interne en quelques heures sans développeur

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `NOCOBASE_ADMIN_EMAIL` | Email du compte administrateur | admin@fluxcaler.net |
| `NOCOBASE_ADMIN_PASSWORD` | Mot de passe administrateur | (généré) |
| `NOCOBASE_APP_KEY` | Clé de signature des sessions | (générée) |
| `NOCOBASE_DB_PASSWORD` | Mot de passe PostgreSQL dédié | (généré) |

## Ports

| Port | Usage |
|------|-------|
| 8085 | Interface web NocoBase |

## Ressources

- [Documentation officielle](https://docs.nocobase.com/)
- [GitHub](https://github.com/nocobase/nocobase)
