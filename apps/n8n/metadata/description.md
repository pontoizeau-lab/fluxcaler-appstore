# n8n - Workflow Automation

## Description

n8n est une plateforme d'automatisation de workflows open-source et auto-hébergeable. Elle permet de connecter différentes applications et services pour automatiser des tâches répétitives grâce à une interface visuelle intuitive.

## Fonctionnalités principales

- **Interface visuelle** : Créez des workflows complexes par glisser-déposer
- **+400 intégrations** : Connectez-vous à des centaines de services (API, bases de données, outils SaaS)
- **Code personnalisé** : Ajoutez du JavaScript/Python pour des logiques avancées
- **Webhooks** : Déclenchez des workflows via des appels HTTP
- **Planification** : Exécutez des workflows à intervalles réguliers (cron)
- **Gestion des erreurs** : Réessais automatiques et notifications d'échec

## Cas d'usage pour Fluxcaler

- Automatisation des pipelines de données
- Orchestration des services IA (Qdrant, Supabase)
- Intégration avec des APIs externes
- ETL et synchronisation de données
- Notifications et alertes automatisées

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `N8N_BASIC_AUTH_USER` | Utilisateur admin | admin |
| `N8N_BASIC_AUTH_PASSWORD` | Mot de passe admin | (généré) |
| `GENERIC_TIMEZONE` | Fuseau horaire | Europe/Paris |
| `WEBHOOK_URL` | URL externe pour webhooks | (optionnel) |

## Ressources

- [Documentation officielle](https://docs.n8n.io/)
- [GitHub](https://github.com/n8n-io/n8n)
- [Communauté](https://community.n8n.io/)
