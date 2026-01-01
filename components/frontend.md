# LobApp Frontend

Le frontend de LobApp est une application web moderne construite avec **Next.js**. Elle offre une interface utilisateur réactive pour explorer les données législatives.

## Stack Technique

- **Framework** : Next.js 16.1 (App Router)
- **Langage** : TypeScript
- **UI & Styling** : React 19, Tailwind CSS 4
- **Gestionnaire de paquets** : npm

## Architecture

L'application suit l'architecture standard Next.js App Router dans `lobapp-front/` :

```
lobapp-front/
├── app/                # Pages et Layouts (App Router)
│   ├── page.tsx        # Page d'accueil
│   ├── layout.tsx      # Layout principal (Header, Footer)
│   └── ...
├── components/         # Composants React réutilisables
│   ├── ui/             # Composants d'interface (Boutons, Cards...)
│   └── ...
├── lib/                # Fonctions utilitaires et configuration API
├── public/             # Assets statiques
└── package.json        # Dépendances et scripts
```

## Fonctionnalités Clés

- **SSR & Server Components** : Utilisation intensive du rendu côté serveur pour la performance et le SEO.
- **Design System** : Interface propre et cohérente grâce à Tailwind CSS.
- **Intégration API** : Consomme l'API FastAPI (`lobapp-back`) pour afficher les données en temps réel.

## Démarrage Local

```bash
cd lobapp-front
# Installer les dépendances
npm install
# Lancer le serveur de développement
npm run dev
```

L'application est accessible sur `http://localhost:3000`.
