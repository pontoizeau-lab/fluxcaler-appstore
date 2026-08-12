# GitLab CE — Forge Git privée + CI/CD

## Qu'est-ce que c'est

GitLab Community Edition est une **forge logicielle complète auto-hébergée** : dépôts Git privés, merge requests, CI/CD, registre de conteneurs, wiki et gestion de tickets — l'équivalent de GitHub, mais sur votre propre serveur.

Sur un VPS Fluxcaler, GitLab est aussi le **point d'ancrage de vos employés IA** : c'est là que vivent leurs dépôts de code, leurs **skills** (compétences versionnées), leurs agents et leurs livrables. Vos assistants IA (Max, agents Claude Code) clonent, committent et ouvrent des merge requests directement sur votre GitLab — sans que votre code ne quitte votre infrastructure.

## Ce qu'il peut faire

- **Dépôts Git privés illimités** : code source, configurations, documents versionnés
- **Merge requests & revue de code** : diff, commentaires, approbations — y compris pour relire le travail de vos employés IA
- **CI/CD intégré** : pipelines de build, tests et déploiement (`.gitlab-ci.yml`)
- **Stockage des skills IA** : chaque skill de vos employés IA est un dépôt versionné (historique, rollback, revue)
- **Connexion employés IA** : accès par token de projet/groupe pour Max et les agents — commits et MR tracés au nom de chaque agent
- **Issues & boards** : tickets, labels, jalons, tableaux kanban par projet
- **Wiki & snippets** : documentation technique au plus près du code
- **Registre de conteneurs** : hébergez vos images Docker privées
- **SSH (port 2222)** : clone/push Git par clé SSH

## Ce qu'il remplace

| Logiciel remplacé | Type |
|---|---|
| **GitHub** | Forge Git cloud |
| **Bitbucket** | Forge Git (Atlassian) |
| **GitLab.com (SaaS)** | Forge Git cloud |
| **Jenkins / CircleCI** | CI/CD |

## Cas d'usage pour Fluxcaler

- Héberger le code et les skills de vos employés IA en toute souveraineté
- Faire travailler Max / Claude Code sur des dépôts privés (clone, commit, merge request)
- CI/CD pour vos scripts, workflows exportés n8n et applications internes

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `GITLAB_EXTERNAL_URL` | URL publique de l'instance | http://localhost:8929 |
| `GITLAB_ROOT_PASSWORD` | Mot de passe initial du compte `root` | (généré) |

Connexion initiale : utilisateur **root** + mot de passe généré (disponible dans l'espace membre).

## Ports

| Port | Usage |
|------|-------|
| 8929 | Interface web GitLab |
| 2222 | Git SSH (clone/push par clé) |

## Ressources requises

⚠️ GitLab est exigeant : ~4 GB de RAM à lui seul. Réservé au plan **Scale**.

## Ressources

- [Documentation officielle](https://docs.gitlab.com/)
- [GitLab CE](https://gitlab.com/gitlab-org/gitlab-foss)
