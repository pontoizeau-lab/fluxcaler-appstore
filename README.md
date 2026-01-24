# Fluxcaler App Store pour Runtipi

Stack d'applications IA souveraine et auto-hébergeable pour [Runtipi](https://runtipi.io/).

## Stack Fluxcaler AI

| Application | Description | Port | Catégorie |
|-------------|-------------|------|-----------|
| **n8n** | Automatisation de workflows visuels | 5678 | Automation |
| **MongoDB** | Base de données documents + Mongo Express | 8081 | Database |
| **Qdrant** | Base de données vectorielle pour IA | 6333, 6334 | AI/Database |
| **Supabase** | Backend complet (Postgres, Auth, REST, Realtime, Storage) | 8000, 3001 | Backend |

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        FLUXCALER STACK                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────┐    ┌──────────────────────────────────────────┐   │
│  │   n8n   │───▶│              ORCHESTRATION               │   │
│  │ :5678   │    │   Workflows • Webhooks • Scheduling      │   │
│  └────┬────┘    └──────────────────────────────────────────┘   │
│       │                                                         │
│       ▼                                                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                      DATA LAYER                          │   │
│  │                                                          │   │
│  │  ┌──────────┐   ┌──────────┐   ┌────────────────────┐   │   │
│  │  │ MongoDB  │   │  Qdrant  │   │     Supabase       │   │   │
│  │  │  :27017  │   │  :6333   │   │  PostgreSQL :5432  │   │   │
│  │  │  :8081   │   │  :6334   │   │  Kong API   :8000  │   │   │
│  │  │ (Express)│   │(Dashboard)│   │  Studio     :3001  │   │   │
│  │  └──────────┘   └──────────┘   └────────────────────┘   │   │
│  │                                                          │   │
│  │  Documents      Vectors/RAG      Auth • REST • Realtime │   │
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

## Applications détaillées

### n8n - Workflow Automation

Plateforme d'automatisation visuelle permettant de créer des workflows complexes sans code.

**Cas d'usage :**
- Pipelines ETL de données
- Intégration d'APIs externes
- Orchestration de services IA
- Automatisation de tâches répétitives

### MongoDB + Mongo Express

Base de données NoSQL orientée documents avec interface d'administration web.

**Cas d'usage :**
- Stockage de configurations JSON
- Logs et événements
- Cache applicatif
- Données semi-structurées

### Qdrant

Base de données vectorielle haute performance pour l'IA et la recherche sémantique.

**Cas d'usage :**
- RAG (Retrieval Augmented Generation)
- Recherche sémantique de documents
- Systèmes de recommandation
- Classification automatique

### Supabase

Alternative open source à Firebase avec PostgreSQL, authentification, APIs automatiques et temps réel.

**Composants inclus :**
- PostgreSQL avec pgvector
- Kong API Gateway
- GoTrue (Auth)
- PostgREST (API REST)
- Realtime (WebSockets)
- Storage (fichiers)
- ImgProxy (transformation images)
- Studio (interface admin)

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
2. Filtrez par catégorie ou recherchez
3. Cliquez sur l'application souhaitée
4. Configurez les paramètres (ports, mots de passe)
5. Cliquez sur **Installer**

## Configuration recommandée

### Ordre d'installation

Pour une stack complète, installez dans cet ordre :

1. **Supabase** - Backend et base PostgreSQL
2. **MongoDB** - Base documents complémentaire
3. **Qdrant** - Base vectorielle pour IA
4. **n8n** - Orchestration (connecter aux services précédents)

### Ressources minimum

| Application | RAM | CPU | Stockage |
|-------------|-----|-----|----------|
| n8n | 512MB | 0.5 | 1GB |
| MongoDB | 1GB | 0.5 | 5GB+ |
| Qdrant | 1GB | 1 | 5GB+ |
| Supabase | 2GB | 2 | 10GB+ |
| **Total** | **4.5GB** | **4** | **21GB+** |

## Intégrations

### n8n vers Supabase

```javascript
// Exemple de node HTTP Request
{
  "url": "http://supabase-kong:8000/rest/v1/table",
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
  "url": "http://qdrant:6333/collections/docs/points/search",
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
"mongodb://admin:password@mongodb:27017/fluxcaler?authSource=admin"
```

## Support

- **Documentation Runtipi** : [docs.runtipi.io](https://docs.runtipi.io/)
- **Issues** : [GitHub Issues](https://github.com/pontoizeau-lab/fluxcaler-appstore/issues)
- **Contributions** : Pull requests bienvenues !

## Licence

MIT - Voir [LICENSE](LICENSE) pour plus de détails.

---

**Fluxcaler** - Infrastructure IA souveraine pour entreprises et développeurs.
