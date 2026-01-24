# MongoDB + Mongo Express

## Description

MongoDB est une base de données NoSQL orientée documents, idéale pour stocker des données semi-structurées et des objets JSON. Ce package inclut Mongo Express, une interface web d'administration pour gérer facilement vos collections.

## Fonctionnalités principales

### MongoDB
- **Documents JSON/BSON** : Stockage flexible de données semi-structurées
- **Requêtes riches** : Filtres, agrégations, recherche texte
- **Indexation** : Index secondaires pour des requêtes performantes
- **Réplication** : Haute disponibilité avec replica sets
- **Sharding** : Scalabilité horizontale pour les gros volumes

### Mongo Express
- **Interface web** : Gestion visuelle des bases et collections
- **CRUD** : Création, lecture, modification, suppression de documents
- **Import/Export** : Support JSON pour la migration de données
- **Statistiques** : Monitoring des performances et de l'espace disque

## Cas d'usage pour Fluxcaler

- Stockage de configurations et métadonnées
- Logs et événements applicatifs
- Cache de données semi-structurées
- Stockage de documents JSON pour les workflows n8n
- Base de données pour applications Node.js

## Configuration

| Variable | Description | Défaut |
|----------|-------------|--------|
| `MONGO_ROOT_USER` | Utilisateur admin MongoDB | admin |
| `MONGO_ROOT_PASSWORD` | Mot de passe admin | (généré) |
| `MONGO_DATABASE` | Base de données par défaut | fluxcaler |
| `ME_BASIC_AUTH_USERNAME` | Utilisateur Mongo Express | admin |
| `ME_BASIC_AUTH_PASSWORD` | Mot de passe Mongo Express | (généré) |

## Connexion

- **Mongo Express** : `http://localhost:8081`
- **MongoDB URI** : `mongodb://admin:password@mongodb:27017/`

## Ressources

- [Documentation MongoDB](https://docs.mongodb.com/)
- [Mongo Express GitHub](https://github.com/mongo-express/mongo-express)
