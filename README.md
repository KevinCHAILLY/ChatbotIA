# Déploiement Pédagogique Ollama + OpenWebUI + n8n

Ce projet permet de déployer une stack pédagogique complète pour l'étude des IA conversationnelles et de l'automatisation avec :
- **Ollama** : Exécution locale de modèles LLM
- **OpenWebUI** : Interface utilisateur pour interagir avec les modèles
- **n8n** : Outil d'automatisation pour créer des workflows

## Prérequis
- Docker installé sur la machine hôte
- Docker Compose (version 2.23.0 ou supérieure)
- Minimum 8 Go de RAM (16 Go recommandés pour de bonnes performances)
- Espace disque suffisant pour les modèles (environ 5 Go par modèle)

## Déploiement

1. **Cloner ce dépôt** (ou copier les fichiers) :
   ```bash
   git clone <ce-depot> chatbot-ia
   cd chatbot-ia
   ```

2. **Démarrer les services** :
   ```bash
   docker compose up -d
   ```

3. **Vérifier le statut** :
   ```bash
   docker compose ps
   ```

## Accès aux services

| Service      | URL                     | Identifiants (si applicable)       |
|--------------|-------------------------|------------------------------------|
| OpenWebUI    | http://localhost:3000   | Inscription libre (ENABLE_SIGNUP=true) |
| n8n          | http://localhost:5678   | admin / pedagogique123             |
| Ollama (API) | http://localhost:11434 | -                                  |

## Configuration pédagogique

### Ollama
- **Modèles disponibles** : Téléchargez des modèles avec la commande :
  ```bash
  docker exec -it ollama ollama pull gpt-oss
  ```
- **Port** : 11434 (API accessible pour les exercices)

### OpenWebUI
- **Configuration** : Les paramètres sont définis dans le `docker-compose.yml`
  - `DEFAULT_MODEL=gpt-oss` : Modèle par défaut
  - `ENABLE_RAG_WEB_SEARCH=true` : Active la recherche web intégrée
  - `RAG_WEB_SEARCH_ENGINE=duckduckgo` : Moteur de recherche utilisé

### n8n
- **Identifiants** : admin / pedagogique123 (modifiables dans le compose)
- **Fonctionnalités pédagogiques** :
  - Création de workflows d'automatisation
  - Intégration avec Ollama via API
  - Gestion des webhooks

## Exemples d'activités pédagogiques

1. **Interaction avec les LLM** :
   - Comparaison des réponses entre différents modèles
   - Analyse des tokens et des coûts de calcul
   - Étude des prompts et du fine-tuning

2. **Automatisation** :
   - Création d'un workflow n8n qui interroge Ollama
   - Automatisation de tâches avec des webhooks
   - Intégration avec d'autres services (email, bases de données)

3. **Déploiement et infrastructure** :
   - Étude de l'architecture Docker
   - Gestion des volumes persistants
   - Configuration réseau entre containers

## Arrêt des services

```bash
# Arrêter les services
docker compose down

# Arrêter et supprimer les volumes (attention : supprime les données)
docker compose down -v
```

## Personnalisation

Modifiez le fichier [`docker-compose.yml`](docker-compose.yml) pour :
- Changer les ports exposés
- Ajouter des modèles Ollama supplémentaires
- Modifier les identifiants n8n
- Configurer des variables d'environnement spécifiques

## Dépannage

- **Problème de mémoire** : Réduisez la taille des modèles ou augmentez la RAM allouée à Docker
- **Ports déjà utilisés** : Modifiez les ports dans le `docker-compose.yml`
- **Problème de connexion** : Vérifiez que tous les services sont bien démarrés avec `docker compose ps`

## Sécurité pédagogique

⚠️ **Ce déploiement est conçu pour un environnement pédagogique** :
- Les identifiants sont en dur dans le fichier de configuration
- La sécurité réseau n'est pas renforcée (réseau bridge local)
- Pour un environnement de production, il faudrait :
  - Utiliser des secrets Docker
  - Configurer un reverse proxy avec HTTPS
  - Mettre en place une authentification forte
  - Isoler le réseau Docker