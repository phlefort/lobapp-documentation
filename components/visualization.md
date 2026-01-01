# LobApp Visualization

Ce composant fournit l'interface utilisateur pour l'exploration des données via **Metabase**.

## Architecture Docker

L'application tourne dans un conteneur Docker pour garantir la portabilité et la facilité de déploiement.

### Configuration (`docker-compose.yml`)

- **Image** : `metabase/metabase:latest`
- **Ports** : `3000:3000` (Accessible via `http://localhost:3000`)
- **Volumes** :
  - La base de données de production est montée en lecture : `../lobapp-transformation/reconciliation.db:/data/reconciliation.db`
  - Les données de configuration Metabase (utilisateurs, dashboards) sont persistées localement : `./metabase-data:/metabase-data`

## Fonctionnalités

Metabase permet de créer :
- Des tableaux de bord de suivi (ex: "Top Influenceurs", "Dossiers les plus actifs").
- Des requêtes SQL personnalisées pour l'analyse approfondie.
- Des visualisations graphiques (camemberts, courbes d'évolution).

## Démarrage

```bash
docker-compose up -d
```
