# Règles de Conception Base de Données

Ces règles s'appliquent strictement à la base de données de production `reconciliation.db` générée par le module **Transformation**.

## 1. Interdiction du JSON (`data_json`)
**Règle** : Aucune colonne ne doit contenir de blob JSON brut.
- Les données doivent être éclatées en colonnes SQL natives (TEXT, INTEGER, DATE, BOOLEAN).
- Cela permet l'indexation, les jointures et l'analyse performante dans Metabase.

## 2. Modèle Relationnel Strict (1:N)
**Règle** : Les listes d'objets imbriqués doivent être extraites dans des tables enfants.
- *Exemple* : Une liste d'activités pour un lobbyiste ne doit pas être stockée dans une seule case. Une table `lobbying_activity` liée par clé étrangère doit être créée.

## 3. Nettoyage à l'Import
**Règle** : Pas de données sales en base.
- Les chaînes de caractères représentant des dictionnaires Python (ex: `"{'id': 1}"`) doivent être parsées avant insertion.
- Les types de données doivent être respectés (pas de dates stockées en string si possible, utiliser le format ISO8601 ou les types natifs SQLite).

## 4. Identifiants
- Utilisation des UIDs originaux (`PA...` pour AN, `SENAT_...` pour Sénat) comme clés de jointure externes.
- Clés étrangères (`FOREIGN KEY`) explicitement déclarées dans le schéma.
