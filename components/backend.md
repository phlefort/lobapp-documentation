# LobApp Backend

Le backend de LobApp est une API REST performante construite avec **FastAPI**. Elle expose les données réconciliées et offre des fonctionnalités de recherche avancée pour le frontend.

## Stack Technique

- **Framework** : FastAPI
- **Langage** : Python 3.x
- **Base de Données** : SQLite (via `aiosqlite` pour l'asynchrone)
- **ORM** : SQLModel (Wrapper autour de SQLAlchemy)
- **Serveur** : Uvicorn

## Architecture

Le code est structuré de manière modulaire dans `lobapp-back/` :

```
lobapp-back/
├── main.py             # Point d'entrée de l'application
├── database.py         # Configuration de la connexion DB (AsyncSession)
├── models.py           # Définitions des modèles SQLModel
├── routers/            # Endpoints de l'API
│   ├── search.py       # Recherche full-text (FTS)
│   ├── dossiers.py     # Endpoints pour les dossiers législatifs
│   ├── acteurs.py      # Endpoints pour les députés et sénateurs
│   └── monitoring.py   # Health checks et stats
└── requirements.txt    # Dépendances Python
```

## Fonctionnalités Clés

### 1. Recherche Full-Text (FTS)
Utilise les capacités FTS5 de SQLite pour permettre une recherche rapide sur les titres et descriptions des dossiers législatifs et des amendements.

### 2. API RESTful
- `GET /search` : Recherche globale.
- `GET /dossiers/{id}` : Détail d'un dossier avec son historique (AN & Sénat).
- `GET /acteurs/{uid}` : Information sur un parlementaire et ses votes.

## Démarrage Local

```bash
cd lobapp-back
# Activer l'environnement virtuel
.\venv\Scripts\activate
# Installer les dépendances
pip install -r requirements.txt
# Lancer le serveur de développement
python -m uvicorn main:app --reload --port 8000
```

La documentation interactive de l'API (Swagger UI) est accessible sur `http://localhost:8000/docs`.
