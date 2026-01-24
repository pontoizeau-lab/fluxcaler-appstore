# Qdrant - Vector Database

## Description

Qdrant est une base de données vectorielle haute performance, conçue pour les applications d'IA et de recherche sémantique. Elle permet de stocker et rechercher des vecteurs d'embeddings avec des métadonnées associées.

## Fonctionnalités principales

- **Recherche vectorielle** : Similarity search avec différentes métriques (cosine, dot, euclidean)
- **Filtrage avancé** : Combinaison de recherche vectorielle et filtres sur métadonnées
- **Collections** : Organisation des données en collections avec schémas flexibles
- **API REST & gRPC** : Interfaces modernes pour l'intégration
- **Dashboard web** : Interface graphique pour explorer les collections
- **Snapshots** : Sauvegarde et restauration des données
- **Quantization** : Compression des vecteurs pour optimiser la mémoire

## Cas d'usage pour Fluxcaler

- **RAG (Retrieval Augmented Generation)** : Stockage d'embeddings pour LLMs
- **Recherche sémantique** : Trouver des documents similaires
- **Recommandations** : Suggérer du contenu basé sur la similarité
- **Classification** : Catégorisation automatique de contenus
- **Détection d'anomalies** : Identifier les outliers dans les données

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `QDRANT_API_KEY` | Clé d'API pour l'authentification | (généré) |
| `QDRANT_ENABLE_GRPC` | Activer l'interface gRPC | true |
| `QDRANT_MAX_COLLECTION_SIZE_MB` | Taille max des collections | 1024 |

## Ports

| Port | Protocole | Description |
|------|-----------|-------------|
| 6333 | HTTP | API REST & Dashboard |
| 6334 | gRPC | Interface haute performance |

## Exemple d'utilisation

```python
from qdrant_client import QdrantClient

client = QdrantClient(
    url="http://localhost:6333",
    api_key="your-api-key"
)

# Créer une collection
client.create_collection(
    collection_name="documents",
    vectors_config={"size": 1536, "distance": "Cosine"}
)

# Recherche vectorielle
results = client.search(
    collection_name="documents",
    query_vector=[0.1, 0.2, ...],
    limit=10
)
```

## Ressources

- [Documentation Qdrant](https://qdrant.tech/documentation/)
- [GitHub](https://github.com/qdrant/qdrant)
- [Tutoriels](https://qdrant.tech/articles/)
