# LobApp Transformation

Ce composant assure la liaison et le nettoyage des données brutes pour produire une base de données analytique propre (`reconciliation.db`).

## Objectif Principal

Le défi majeur est de relier les dossiers législatifs qui portent des identifiants différents à l'Assemblée Nationale et au Sénat ("Navette Parlementaire").

## Algorithme de Réconciliation

La réconciliation est effectuée par `reconciliation_service.py` selon la logique suivante :

1.  **Priorité au Code NOR** :
    - Si un dossier possède un code NOR (Numéro d'Objet de Réglementation) à l'AN et au Sénat, ils sont liés de manière déterministe.

2.  **Matching par Titre (Fuzzy Matching)** :
    - En l'absence de NOR commun, le système compare les titres normalisés.
    - **Normalisation** : Minuscules, suppression des accents, retrait des mentions types ("projet de loi", "proposition de loi").
    - Si les titres normalisés correspondent, les dossiers sont liés.

## Structure de la Base de Données (`reconciliation.db`)

La base finale suit des règles strictes (voir [Règles de Schéma](../schematics/database_schema.md)).

### Tables Clés

- **`legislative_file`** : Table pivot représentant un dossier unique réconcilié.
- **`an_dossier_link`** : Pointeur vers le dossier source AN.
- **`senat_dossier_link`** : Pointeur vers le dossier source Sénat.

### Commandes Principales

```bash
# Initialiser la base
python init_db.py

# Lancer la réconciliation
python run_reconciliation.py

# Générer des rapports (CSV/JSON)
python export_reconciliation.py
```
