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

## Modèles de Données

Le backend utilise **SQLModel** pour gérer 5 tables principales :

### `Actor`
Représente un acteur politique (député, sénateur).
- `uid` : Identifiant unique (clé primaire)
- `nom`, `prenom`, `civ` : Informations d'identité

### `LegislativeFile`
Dossier législatif parlementaire avec titre et code NOR.

### `Amendment`
Amendements législatifs liés aux dossiers, avec texte, dispositif et statut.

### `AmendmentAuthor`
Table de liaison many-to-many entre `Amendment` et `Actor`.

### `QuestionParlementaire`
Questions parlementaires posées par les acteurs avec texte de question et réponse.

## Fonctionnalités Clés

### 1. Recherche Full-Text (FTS)
Utilise les capacités FTS5 de SQLite pour permettre une recherche rapide sur les titres et descriptions des dossiers législatifs et des amendements.

### 2. API RESTful

#### `/acteurs`
- `GET /acteurs/` : Liste paginée avec recherche par nom/prénom
  - Paramètres : `q` (recherche), `page`, `per_page`
  - Retourne : liste d'acteurs avec pagination
- `GET /acteurs/{actor_id}` : Détails d'un acteur avec statistiques
  - Inclut : nombre d'amendements et de questions parlementaires

#### `/dossiers`
- `GET /dossiers/{id}` : Détail d'un dossier avec son historique (AN & Sénat)

#### `/search`
- `GET /search` : Recherche globale full-text

#### `/monitoring`
- Health checks et statistiques système

## Démarrage Local

```bash
cd lobapp-back
# Activer l'environnement virtuel
.\venv\Scripts\activate
# Installer les dépendances
pip install -r requirements.txt
# Lancer le serveur de développement
python -m uvicorn main:app --reload --port 8001
```

La documentation interactive de l'API (Swagger UI) est accessible sur `http://localhost:8001/docs`.

## Configuration

### CORS
Le middleware CORS est configuré en mode permissif (`allow_origins=["*"]`) pour le développement. En production, restreindre aux origines autorisées.

### Base de Données
La base de données `legi_data.db` est créée automatiquement au démarrage via SQLModel. Elle est alimentée par le pipeline `lobapp-transformation`.

