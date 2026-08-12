# Twenty — CRM moderne open source

## Qu'est-ce que c'est

Twenty est un **CRM open source moderne** (interface inspirée de Notion) pour gérer contacts, entreprises, opportunités et pipelines de vente. C'est l'alternative souveraine aux CRM SaaS américains : vos données clients restent sur votre serveur.

## Ce qu'il peut faire

- **Contacts & entreprises** : fiches enrichies, champs personnalisés, notes, tâches, fichiers joints
- **Pipelines de vente** : opportunités en vue kanban ou tableau, étapes personnalisables
- **Objets personnalisés** : modélisez vos propres entités (projets, abonnements, tickets…)
- **Vues flexibles** : filtres, tris, regroupements sauvegardés par équipe
- **Emails & calendrier** : synchronisation Gmail / Outlook (IMAP), timeline d'activité par contact
- **API GraphQL & REST + webhooks** : intégration directe avec vos workflows n8n
- **Multi-utilisateurs** : espaces de travail, rôles, invitations d'équipe

## Ce qu'il remplace

| Logiciel remplacé | Type |
|---|---|
| **Salesforce** | CRM entreprise |
| **HubSpot CRM** | CRM marketing/ventes |
| **Pipedrive** | Pipeline commercial |
| **Attio / Folk** | CRM nouvelle génération |

## Cas d'usage pour Fluxcaler

- Centraliser prospects et clients alimentés automatiquement par n8n (formulaires, emails, paiements)
- Piloter le pipeline commercial de l'équipe avec des données 100% souveraines
- Déclencher des workflows n8n sur chaque changement d'étape (webhooks Twenty)

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `TWENTY_SERVER_URL` | URL publique de l'instance | http://localhost:8086 |
| `TWENTY_APP_SECRET` | Secret applicatif (tokens) | (généré) |
| `TWENTY_DB_PASSWORD` | Mot de passe PostgreSQL dédié | (généré) |

Le compte administrateur se crée **au premier accès** à l'interface (bouton « Sign up ») — utilisez votre email principal.

## Ports

| Port | Usage |
|------|-------|
| 8086 | Interface web Twenty |

## Ressources

- [Documentation officielle](https://twenty.com/developers)
- [GitHub](https://github.com/twentyhq/twenty)
