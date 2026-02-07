# Nextcloud - File Management

## Description

Instance Nextcloud pour la gestion de fichiers clients Fluxcaler. Partage de documents, fichiers projet et collaboration. Accessible via Cloudflare Tunnel sur files.{domain}.

## Fonctionnalites principales

- **Partage de fichiers** : Partagez des documents avec vos clients et collaborateurs
- **Synchronisation** : Synchronisez vos fichiers sur tous vos appareils
- **Collaboration** : Editez des documents en temps reel avec Collabora/OnlyOffice
- **Calendrier & Contacts** : CalDAV et CardDAV integres
- **Applications** : Extensible avec des centaines d'applications tierces
- **Securite** : Chiffrement cote serveur, authentification 2FA

## Cas d'usage pour Fluxcaler

- Partage de documents projet avec les clients
- Stockage centralise de fichiers d'entreprise
- Collaboration sur des documents en temps reel
- Sauvegarde et archivage de donnees

## Configuration

| Variable | Description | Defaut |
|----------|-------------|--------|
| `NEXTCLOUD_ADMIN_USER` | Utilisateur administrateur | admin |
| `NEXTCLOUD_ADMIN_PASSWORD` | Mot de passe administrateur | (genere) |

## Ports

| Port | Usage |
|------|-------|
| 8890 | Interface web Nextcloud |

## Ressources

- [Documentation officielle](https://docs.nextcloud.com/)
- [GitHub](https://github.com/nextcloud/server)
- [Communaute](https://help.nextcloud.com/)
