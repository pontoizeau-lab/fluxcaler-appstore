# Fluxcaler App Store pour Runtipi

Stack d'applications IA souveraine et auto-hébergeable pour [Runtipi](https://runtipi.io/).

## Stack Fluxcaler AI

| Application | Description | Port | Catégorie |
|-------------|-------------|------|-----------|
| **fluxcaler-n8n** | Automatisation de workflows visuels | 5679 | Automation |
| **fluxcaler-mongodb** | Base de données documents + Mongo Express | 27018, 8082 | Database |
| **fluxcaler-qdrant** | Base de données vectorielle pour IA | 6335, 6336 | AI/Database |
| **fluxcaler-supabase** | Backend complet (Postgres, Auth, REST, Realtime, Storage) | 8010, 8444, 3002, 5433 | Backend |

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        FLUXCALER STACK                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────────┐    ┌──────────────────────────────────────┐   │
│  │ fluxcaler-  │───▶│              ORCHESTRATION           │   │
│  │    n8n      │    │   Workflows • Webhooks • Scheduling  │   │
│  │   :5679     │    └──────────────────────────────────────┘   │
│  └─────┬───────┘                                                │
│        │                                                        │
│        ▼                                                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                      DATA LAYER                          │   │
│  │                                                          │   │
│  │  ┌──────────────┐ ┌──────────────┐ ┌─────────────────┐  │   │
│  │  │  fluxcaler-  │ │  fluxcaler-  │ │   fluxcaler-    │  │   │
│  │  │   mongodb    │ │    qdrant    │ │    supabase     │  │   │
│  │  │   :27018     │ │    :6335     │ │  Postgres :5433 │  │   │
│  │  │   :8082      │ │    :6336     │ │  Kong API :8010 │  │   │
│  │  │  (Express)   │ │  (Dashboard) │ │  Studio   :3002 │  │   │
│  │  └──────────────┘ └──────────────┘ └─────────────────┘  │   │
│  │                                                          │   │
│  │  Documents        Vectors/RAG      Auth • REST • Realtime│   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

## Avantages Souveraineté

### 100% Auto-hébergé

- **Contrôle total des données** : Aucune donnée ne quitte votre infrastructure
- **Pas de dépendance cloud** : Fonctionne hors-ligne, sans connexion externe
- **RGPD compliant** : Maîtrise complète du stockage et traitement des données
- **Coûts prévisibles** : Pas de facturation à l'usage ou surprises

### Open Source

- **Code auditable** : Toutes les applications sont open source
- **Pas de vendor lock-in** : Migration facile, formats standards
- **Communauté active** : Support communautaire et évolutions continues
- **Personnalisable** : Adaptez chaque composant à vos besoins

### Sécurité

- **Réseau isolé** : Communication inter-services via réseau Docker privé
- **Authentification** : Chaque service dispose de son propre système d'auth
- **Chiffrement** : Support TLS/SSL pour toutes les connexions
- **Mises à jour contrôlées** : Vous décidez quand mettre à jour

### Aucun conflit de ports

- **Préfixe fluxcaler-** : Toutes les apps sont préfixées pour éviter les conflits
- **Ports décalés** : Ports uniques pour cohabiter avec d'autres installations
- **Isolation complète** : Fonctionne indépendamment de l'app store officiel

## Applications détaillées

### fluxcaler-n8n - Workflow Automation

Plateforme d'automatisation visuelle permettant de créer des workflows complexes sans code.

**Cas d'usage :**
- Pipelines ETL de données
- Intégration d'APIs externes
- Orchestration de services IA
- Automatisation de tâches répétitives

### fluxcaler-mongodb - MongoDB + Mongo Express

Base de données NoSQL orientée documents avec interface d'administration web.

**Cas d'usage :**
- Stockage de configurations JSON
- Logs et événements
- Cache applicatif
- Données semi-structurées

### fluxcaler-qdrant - Vector Database

Base de données vectorielle haute performance pour l'IA et la recherche sémantique.

**Cas d'usage :**
- RAG (Retrieval Augmented Generation)
- Recherche sémantique de documents
- Systèmes de recommandation
- Classification automatique

### fluxcaler-supabase - Backend Complet

Alternative open source à Firebase avec PostgreSQL, authentification, APIs automatiques et temps réel.

**Composants inclus :**
- PostgreSQL avec pgvector (port 5433)
- Kong API Gateway (port 8010, 8444)
- GoTrue (Auth)
- PostgREST (API REST)
- Realtime (WebSockets)
- Storage (fichiers)
- ImgProxy (transformation images)
- Studio (interface admin, port 3002)

## Installation rapide

### Prérequis

- [Runtipi](https://runtipi.io/) installé
- Docker et Docker Compose
- Minimum 4GB RAM recommandé (8GB+ pour Supabase complet)

### Ajout du repository

1. Accédez aux **Paramètres** de Runtipi
2. Section **App Stores**
3. Ajoutez l'URL : `https://github.com/pontoizeau-lab/fluxcaler-appstore`
4. Cliquez sur **Ajouter**

### Installation des apps

1. Allez dans l'**App Store**
2. Filtrez par catégorie ou recherchez "fluxcaler"
3. Cliquez sur l'application souhaitée
4. Configurez les paramètres (ports, mots de passe)
5. Cliquez sur **Installer**

## Configuration recommandée

### Ordre d'installation

Pour une stack complète, installez dans cet ordre :

1. **fluxcaler-supabase** - Backend et base PostgreSQL
2. **fluxcaler-mongodb** - Base documents complémentaire
3. **fluxcaler-qdrant** - Base vectorielle pour IA
4. **fluxcaler-n8n** - Orchestration (connecter aux services précédents)

### Ressources minimum

| Application | RAM | CPU | Stockage |
|-------------|-----|-----|----------|
| fluxcaler-n8n | 512MB | 0.5 | 1GB |
| fluxcaler-mongodb | 1GB | 0.5 | 5GB+ |
| fluxcaler-qdrant | 1GB | 1 | 5GB+ |
| fluxcaler-supabase | 2GB | 2 | 10GB+ |
| **Total** | **4.5GB** | **4** | **21GB+** |

## Intégrations

### n8n vers Supabase

```javascript
// Exemple de node HTTP Request
{
  "url": "http://fluxcaler-supabase-kong:8000/rest/v1/table",
  "headers": {
    "apikey": "{{$env.SUPABASE_ANON_KEY}}",
    "Authorization": "Bearer {{$env.SUPABASE_ANON_KEY}}"
  }
}
```

### n8n vers Qdrant

```javascript
// Recherche vectorielle
{
  "url": "http://fluxcaler-qdrant:6333/collections/docs/points/search",
  "headers": {
    "api-key": "{{$env.QDRANT_API_KEY}}"
  },
  "body": {
    "vector": [0.1, 0.2, ...],
    "limit": 10
  }
}
```

### n8n vers MongoDB

```javascript
// Connection string
"mongodb://admin:password@fluxcaler-mongodb:27017/fluxcaler?authSource=admin"
```

## Mapping des ports

| Service | Port standard | Port Fluxcaler |
|---------|---------------|----------------|
| n8n | 5678 | 5679 |
| MongoDB | 27017 | 27018 |
| Mongo Express | 8081 | 8082 |
| Qdrant REST | 6333 | 6335 |
| Qdrant gRPC | 6334 | 6336 |
| Supabase Kong | 8000 | 8010 |
| Supabase Kong SSL | 8443 | 8444 |
| Supabase Studio | 3001 | 3002 |
| Supabase Postgres | 5432 | 5433 |

## Support

- **Documentation Runtipi** : [docs.runtipi.io](https://docs.runtipi.io/)
- **Issues** : [GitHub Issues](https://github.com/pontoizeau-lab/fluxcaler-appstore/issues)
- **Contributions** : Pull requests bienvenues !

## Licence

MIT - Voir [LICENSE](LICENSE) pour plus de détails.

---

**Fluxcaler** - Infrastructure IA souveraine pour entreprises et développeurs.
