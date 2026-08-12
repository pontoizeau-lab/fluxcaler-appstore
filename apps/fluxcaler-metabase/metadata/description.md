# Metabase — Business Intelligence & Dashboards

## Qu'est-ce que c'est

Metabase est une plateforme de **Business Intelligence (BI) open source** : elle se connecte à vos bases de données (PostgreSQL, MySQL, MongoDB…) et permet d'explorer les données, de poser des questions **sans écrire de SQL** et de construire des tableaux de bord partageables.

## Ce qu'il peut faire

- **Explorer sans SQL** : l'éditeur visuel de questions permet à un non-technicien de filtrer, agréger et croiser les données
- **Dashboards interactifs** : graphiques, KPI, tableaux, cartes — avec filtres dynamiques et actualisation automatique
- **SQL natif** : les analystes gardent un éditeur SQL complet avec variables et snippets
- **Alertes et abonnements** : envoi automatique de rapports par email ou Slack quand un seuil est franchi
- **Multi-sources** : connectez en parallèle votre Supabase locale, MongoDB, ou toute base externe
- **Permissions** : groupes, accès par base / schéma / table, sandboxing des données
- **Embedding** : intégration de graphiques dans vos propres applications

## Ce qu'il remplace

| Logiciel remplacé | Type |
|---|---|
| **Tableau** | BI / visualisation de données |
| **Microsoft Power BI** | BI / reporting |
| **Looker (Google)** | BI cloud |
| **Google Data Studio / Looker Studio** | Dashboards |

## Cas d'usage pour Fluxcaler

- Visualiser les données produites par vos workflows n8n (ventes, leads, opérations)
- Brancher la Supabase locale ou MongoDB du VPS et construire vos KPI métier
- Rapports automatiques hebdomadaires envoyés à l'équipe

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `METABASE_SITE_URL` | URL publique de l'instance | http://localhost:8084 |
| `METABASE_DB_PASSWORD` | Mot de passe PostgreSQL (base applicative) | (généré) |

Le compte administrateur est créé automatiquement au provisioning (email du client) ; le mot de passe est disponible dans l'espace membre.

## Ports

| Port | Usage |
|------|-------|
| 8084 | Interface web Metabase |

## Ressources

- [Documentation officielle](https://www.metabase.com/docs/latest/)
- [GitHub](https://github.com/metabase/metabase)
