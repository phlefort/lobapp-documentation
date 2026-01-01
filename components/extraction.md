# LobApp Extraction

Ce composant est responsable de la récupération des données ouvertes depuis les sources officielles et de leur chargement dans une base de données SQLite intermédiaire (`legi_data.db`).

## Sources de Données

### 1. Assemblée Nationale (Open Data)
Données récupérées au format JSON.
- **Acteurs** : Députés, organes parlementaires.
- **Dossiers Législatifs** : Historique des textes de loi (Législatures 16 & 17).
- **Questions** : Questions écrites et orales.
- **Scrutins** : Détail des votes solennels et publics.
- **Amendements** : Texte et statut des amendements.

### 2. Sénat (Open Data)
Données récupérées via des dumps SQL fournis par le Sénat.
- **Ameli** : Amendements.
- **Dosleg** : Dossiers législatifs.
- **Questions** : Questions parlementaires.
- **Sens** : Informations sur les Sénateurs.

### 3. HATVP (Haute Autorité pour la Transparence de la Vie Publique)
Données récupérées via des exports CSV/XML.
- **Répertoire** : Informations sur les représentants d'intérêts, leurs activités de lobbying, et les décisions visées.

## Architecture Technique

Le dossier `scripts/` contient les modules d'ingestion :

- `sqlite_ingester_an.py` : Parsers pour les fichiers JSON de l'AN.
- `sqlite_ingester_senat.py` : Importateur pour les dumps SQL du Sénat.
- `sqlite_ingester_hatvp_csv.py` : Traitement des fichiers plats HATVP.

### Pipeline d'Exécution

L'ingestion peut être lancée module par module :
```bash
# Exemple pour les acteurs de l'AN
python scripts/run_an_acteurs.py

# Exemple pour les données du Sénat
python scripts/run_senat_ameli.py
```

## Sortie

Les données sont consolidées dans `output_data/legi_data.db`. Les tables sont préfixées pour indiquer leur origine :
- `an_*`
- `senat_*`
- `hatvp_*`
