# Supabase - Backend complet

## Description

Supabase est une alternative open source à Firebase. Il fournit une suite complète de services backend : base de données PostgreSQL, authentification, APIs REST automatiques, temps réel, stockage de fichiers et support des embeddings vectoriels.

## Architecture

Cette installation inclut tous les composants Supabase :

| Service | Description | Port |
|---------|-------------|------|
| **PostgreSQL** | Base de données principale | 5432 |
| **Kong** | API Gateway | 8000 |
| **GoTrue** | Authentification | 9999 |
| **PostgREST** | API REST auto-générée | 3000 |
| **Realtime** | Websockets & subscriptions | 4000 |
| **Storage** | Stockage de fichiers | 5000 |
| **ImgProxy** | Transformation d'images | 5001 |
| **Meta** | Métadonnées PostgreSQL | 8080 |
| **Studio** | Interface d'administration | 3001 |

## Fonctionnalités principales

### Base de données
- PostgreSQL avec extensions (pgvector, pg_stat, etc.)
- Row Level Security (RLS) pour la sécurité
- Migrations et versionning

### Authentification
- Email/Password, Magic Links
- OAuth (Google, GitHub, etc.)
- JWT tokens
- Multi-factor authentication

### APIs
- REST auto-générée depuis le schéma PostgreSQL
- GraphQL disponible
- Subscriptions temps réel

### Stockage
- Upload/download de fichiers
- Transformation d'images à la volée
- Politiques d'accès par bucket

### Vector / IA
- Extension pgvector incluse
- Stockage d'embeddings
- Recherche de similarité

## Cas d'usage pour Fluxcaler

- **Backend d'applications** : Auth + Database + Storage intégrés
- **APIs instantanées** : Exposition automatique des tables PostgreSQL
- **Temps réel** : Notifications push, chat, collaboration
- **RAG avec pgvector** : Stockage d'embeddings pour LLMs
- **Stockage de médias** : Images, documents, fichiers

## Configuration

| Variable | Description |
|----------|-------------|
| `SITE_URL` | URL publique de l'application |
| `POSTGRES_PASSWORD` | Mot de passe PostgreSQL |
| `JWT_SECRET` | Secret pour les tokens JWT |
| `ANON_KEY` | Clé publique (anon) |
| `SERVICE_ROLE_KEY` | Clé admin (service_role) |
| `DASHBOARD_USERNAME` | Utilisateur Studio |
| `DASHBOARD_PASSWORD` | Mot de passe Studio |

## Accès

- **Kong API** : `http://localhost:8000`
- **Studio** : `http://localhost:3001`
- **PostgreSQL** : `postgresql://postgres:password@localhost:5432/postgres`

## Exemple d'utilisation

```javascript
import { createClient } from '@supabase/supabase-js'

const supabase = createClient(
  'http://localhost:8000',
  'your-anon-key'
)

// Authentification
await supabase.auth.signUp({
  email: 'user@example.com',
  password: 'password123'
})

// Query
const { data } = await supabase
  .from('users')
  .select('*')

// Realtime
supabase
  .channel('changes')
  .on('postgres_changes', { event: '*', schema: 'public' }, console.log)
  .subscribe()
```

## Ressources

- [Documentation Supabase](https://supabase.com/docs)
- [GitHub](https://github.com/supabase/supabase)
- [Guides](https://supabase.com/docs/guides)
