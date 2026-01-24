# Guide de déploiement Fluxcaler App Store

Ce guide détaille le déploiement du Fluxcaler App Store sur Runtipi.

## Table des matières

1. [Prérequis](#prérequis)
2. [Installation de Runtipi](#installation-de-runtipi)
3. [Configuration du repository](#configuration-du-repository)
4. [Installation des applications](#installation-des-applications)
5. [Configuration post-installation](#configuration-post-installation)
6. [Dépannage](#dépannage)

## Prérequis

### Matériel minimum

- **CPU** : 4 cores (8 recommandé)
- **RAM** : 8GB minimum (16GB recommandé pour la stack complète)
- **Stockage** : 50GB SSD minimum
- **Réseau** : Connexion stable, ports ouverts si exposition externe

### Logiciels requis

- **Système** : Linux (Ubuntu 22.04+, Debian 11+, ou compatible)
- **Docker** : Version 24.0+
- **Docker Compose** : Version 2.20+
- **Git** : Pour cloner le repository

### Vérification des prérequis

```bash
# Version Docker
docker --version

# Version Docker Compose
docker compose version

# Espace disque
df -h

# Mémoire disponible
free -h
```

## Installation de Runtipi

### Installation automatique

```bash
# Télécharger et exécuter l'installateur
curl -L https://setup.runtipi.io | bash
```

### Installation manuelle

```bash
# Cloner Runtipi
git clone https://github.com/runtipi/runtipi.git
cd runtipi

# Lancer l'installation
sudo ./scripts/install.sh
```

### Accès au dashboard

Après installation, accédez à Runtipi :
- URL : `http://votre-ip:80` ou `http://localhost:80`
- Créez votre compte administrateur lors du premier accès

## Configuration du repository

### Méthode 1 : Via l'interface Runtipi

1. Connectez-vous au dashboard Runtipi
2. Cliquez sur **Settings** (icône engrenage)
3. Section **App Repositories**
4. Cliquez sur **Add Repository**
5. Entrez l'URL : `https://github.com/pontoizeau-lab/fluxcaler-appstore`
6. Cliquez sur **Add**
7. Attendez la synchronisation (quelques secondes)

### Méthode 2 : Via la configuration

Éditez le fichier de configuration Runtipi :

```bash
# Ouvrir la configuration
nano /opt/runtipi/state/settings.json
```

Ajoutez le repository :

```json
{
  "appStores": [
    {
      "url": "https://github.com/pontoizeau-lab/fluxcaler-appstore",
      "enabled": true
    }
  ]
}
```

Redémarrez Runtipi :

```bash
cd /opt/runtipi
sudo ./scripts/restart.sh
```

## Installation des applications

### Ordre recommandé

Pour une intégration optimale, installez les apps dans cet ordre :

1. **fluxcaler-supabase** (base de données principale)
2. **fluxcaler-mongodb** (base documents)
3. **fluxcaler-qdrant** (base vectorielle)
4. **fluxcaler-n8n** (orchestration)

### Installation de fluxcaler-supabase

1. Dans l'App Store, recherchez **fluxcaler-supabase**
2. Cliquez sur **Install**
3. Configurez les paramètres :

| Paramètre | Description | Recommandation |
|-----------|-------------|----------------|
| `SITE_URL` | URL publique | `https://votre-domaine.com` |
| `POSTGRES_PASSWORD` | Mot de passe PostgreSQL | Générer automatiquement |
| `JWT_SECRET` | Secret JWT (32+ chars) | Générer automatiquement |
| `ANON_KEY` | Clé publique | Générer automatiquement |
| `SERVICE_ROLE_KEY` | Clé admin | Générer automatiquement |
| `DASHBOARD_USERNAME` | Utilisateur Studio | `admin` |
| `DASHBOARD_PASSWORD` | Mot de passe Studio | Complexe, 12+ chars |

4. Cliquez sur **Install**
5. Attendez le démarrage (2-5 minutes)

**Ports exposés :**
- API Gateway : `8010` (HTTP), `8444` (HTTPS)
- Studio : `3002`
- PostgreSQL : `5433`

**Important** : Notez les clés générées, elles seront nécessaires pour les intégrations.

### Installation de fluxcaler-mongodb

1. Recherchez **fluxcaler-mongodb** dans l'App Store
2. Configurez :

| Paramètre | Recommandation |
|-----------|----------------|
| `MONGO_ROOT_USER` | `admin` |
| `MONGO_ROOT_PASSWORD` | Générer |
| `MONGO_DATABASE` | `fluxcaler` |
| `ME_BASIC_AUTH_USERNAME` | `admin` |
| `ME_BASIC_AUTH_PASSWORD` | Générer |

3. Installez et vérifiez via Mongo Express

**Ports exposés :**
- MongoDB : `27018`
- Mongo Express : `8082`

### Installation de fluxcaler-qdrant

1. Recherchez **fluxcaler-qdrant** dans l'App Store
2. Configurez :

| Paramètre | Recommandation |
|-----------|----------------|
| `QDRANT_API_KEY` | Générer (16+ chars) |
| `QDRANT_ENABLE_GRPC` | `true` |

3. Installez et vérifiez via le dashboard (`http://ip:6335/dashboard`)

**Ports exposés :**
- REST API : `6335`
- gRPC : `6336`

### Installation de fluxcaler-n8n

1. Recherchez **fluxcaler-n8n** dans l'App Store
2. Configurez :

| Paramètre | Recommandation |
|-----------|----------------|
| `N8N_BASIC_AUTH_USER` | `admin` |
| `N8N_BASIC_AUTH_PASSWORD` | Générer |
| `GENERIC_TIMEZONE` | `Europe/Paris` |
| `WEBHOOK_URL` | URL externe si webhooks publics |

3. Installez et accédez à l'interface

**Port exposé :** `5679`

## Configuration post-installation

### Connexion n8n vers les services

#### Credentials Supabase dans n8n

1. Dans n8n, allez dans **Settings** > **Credentials**
2. Créez un nouveau credential **Supabase API**
3. Configurez :
   - **Host** : `http://fluxcaler-supabase-kong:8000`
   - **Service Role Key** : Votre `SERVICE_ROLE_KEY`

#### Credentials Qdrant dans n8n

1. Créez un credential **HTTP Header Auth**
2. Configurez :
   - **Name** : `api-key`
   - **Value** : Votre `QDRANT_API_KEY`

#### Credentials MongoDB dans n8n

1. Créez un credential **MongoDB**
2. Configurez :
   - **Connection String** : `mongodb://admin:password@fluxcaler-mongodb:27017/?authSource=admin`

### Vérification des services

```bash
# Status des conteneurs
docker ps --filter "name=fluxcaler"

# Logs d'un service
docker logs -f runtipi-fluxcaler-n8n

# Santé des services
curl http://localhost:5679/healthz      # n8n
curl http://localhost:6335/readyz       # Qdrant
curl http://localhost:8010/rest/v1/     # Supabase
```

### Configuration DNS (optionnel)

Pour un accès externe, configurez vos DNS :

```
n8n.votre-domaine.com      -> IP:5679
supabase.votre-domaine.com -> IP:8010
studio.votre-domaine.com   -> IP:3002
mongo.votre-domaine.com    -> IP:8082
qdrant.votre-domaine.com   -> IP:6335
```

### Reverse Proxy avec Traefik (optionnel)

Runtipi inclut Traefik. Pour exposer les apps :

1. Dans les paramètres de chaque app, activez **Expose**
2. Configurez le domaine
3. Le certificat SSL sera automatique via Let's Encrypt

## Sauvegardes

### Sauvegarde manuelle

```bash
# Localisation des données
ls /opt/runtipi/app-data/

# Sauvegarde complète
tar -czvf fluxcaler-backup-$(date +%Y%m%d).tar.gz \
  /opt/runtipi/app-data/fluxcaler-n8n \
  /opt/runtipi/app-data/fluxcaler-mongodb \
  /opt/runtipi/app-data/fluxcaler-qdrant \
  /opt/runtipi/app-data/fluxcaler-supabase
```

### Restauration

```bash
# Arrêter les apps dans Runtipi d'abord
# Puis restaurer
tar -xzvf fluxcaler-backup-YYYYMMDD.tar.gz -C /
```

## Dépannage

### Problèmes courants

#### L'application ne démarre pas

```bash
# Vérifier les logs
docker logs runtipi-fluxcaler-<app-name>

# Vérifier les ressources
docker stats
```

#### Erreurs de connexion entre services

Les services communiquent via le réseau Docker `runtipi_tipi_main_network`. Vérifiez :

```bash
# Lister le réseau
docker network inspect runtipi_tipi_main_network

# Tester la connectivité
docker exec runtipi-fluxcaler-n8n ping fluxcaler-mongodb
```

#### Supabase ne démarre pas complètement

Supabase a de nombreux services dépendants. Vérifiez l'ordre de démarrage :

```bash
# Vérifier tous les conteneurs Supabase
docker ps -a | grep fluxcaler-supabase

# Redémarrer dans l'ordre
docker restart fluxcaler-supabase-db
sleep 10
docker restart fluxcaler-supabase-auth fluxcaler-supabase-rest
sleep 5
docker restart fluxcaler-supabase-kong
```

#### Manque de mémoire

```bash
# Vérifier la mémoire
free -h

# Augmenter le swap si nécessaire
sudo fallocate -l 4G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
```

### Mapping des ports (référence rapide)

| Service | Port Fluxcaler |
|---------|----------------|
| n8n | 5679 |
| MongoDB | 27018 |
| Mongo Express | 8082 |
| Qdrant REST | 6335 |
| Qdrant gRPC | 6336 |
| Supabase Kong | 8010 |
| Supabase Kong SSL | 8444 |
| Supabase Studio | 3002 |
| Supabase Postgres | 5433 |

### Support

- **Documentation Runtipi** : [docs.runtipi.io](https://docs.runtipi.io/)
- **Issues Fluxcaler** : [GitHub Issues](https://github.com/pontoizeau-lab/fluxcaler-appstore/issues)
- **Communauté** : Discussions GitHub

---

**Fluxcaler** - Déployez votre infrastructure IA en toute souveraineté.
