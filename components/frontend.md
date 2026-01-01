# LobApp Frontend

Le frontend de LobApp est une application web moderne construite avec **Next.js**. Elle offre deux interfaces distinctes : une section publique pour explorer les données législatives, et une interface professionnelle pour les représentants d'intérêts.

## Stack Technique

- **Framework** : Next.js 16.1 (App Router)
- **Langage** : TypeScript
- **UI & Styling** : React 19, Tailwind CSS 4
- **Gestionnaire de paquets** : npm

## Architecture

L'application suit l'architecture Next.js App Router avec deux sections principales :

```
lobapp-front/
├── app/                      # Pages et Layouts (App Router)
│   ├── (public)/             # Section publique
│   │   ├── page.tsx          # Dashboard / Accueil
│   │   ├── acteurs/          # Annuaire des acteurs politiques
│   │   ├── dossiers/         # Détails des dossiers législatifs
│   │   └── search/           # Recherche avancée
│   ├── manager/              # Interface de gestion HATVP
│   │   ├── page.tsx          # Dashboard manager
│   │   ├── clients/          # Gestion des dossiers clients
│   │   ├── reports/          # Générateur de livrables
│   │   └── texts/            # Suivi des textes législatifs
│   ├── recherche/            # Page recherche avancée
│   └── layout.tsx            # Layout racine
├── components/               # Composants React réutilisables
│   ├── Navbar.tsx            # Navigation publique
│   ├── TopNavbar.tsx         # Navigation manager
│   ├── Sidebar.tsx           # Menu latéral manager
│   ├── SearchBar.tsx         # Recherche
│   ├── acteurs/              # Composants acteurs
│   ├── advanced-search/      # Composants recherche
│   ├── dashboard/            # Composants dashboard
│   ├── elu/                  # Composants profil élu
│   └── manager/              # Composants manager
├── lib/                      # Utilitaires et config API
└── public/                   # Assets statiques
```

## Fonctionnalités Clés

### Section Publique

- **Dashboard** : Statistiques clés et tendances législatives
- **Annuaire des Acteurs** (`/acteurs`) : Liste paginée avec recherche, cartes interactives
- **Profil d'Élu** (`/acteurs/[id]`) : En-tête, statistiques, biographie, timeline d'activité
- **Détails Dossier** (`/dossiers/[id]`) : Informations complètes sur un dossier législatif
- **Recherche Avancée** (`/recherche`) : Filtres multi-critères avec pagination

### Section Manager

Interface professionnelle pour les représentants d'intérêts :

- **Dashboard Manager** : Vue d'ensemble des dossiers clients
- **Gestion Dossiers Clients** (`/manager/clients`) : Suivi des échéances et actions
- **Générateur de Livrables** (`/manager/reports`) : Création de rapports personnalisables
- **Suivi des Textes** (`/manager/texts`) : Monitoring législatif en temps réel

### Composants Réutilisables

- **Navigation** : `Navbar` (public), `TopNavbar` + `Sidebar` (manager)
- **Cartes** : `ActorCard`, `StatsCard`, `ResultCard`
- **Recherche** : `SearchBar`, `FilterPanel`
- **Affichage** : `ActivityTimeline`, layout components

## Technologies UI

- **SSR & Server Components** : Rendu côté serveur pour performance et SEO
- **Design System** : Interface cohérente avec Tailwind CSS 4
- **Intégration API** : Consomme l'API FastAPI (`lobapp-back`) sur `http://127.0.0.1:8001`

## Démarrage Local

```bash
cd lobapp-front
# Installer les dépendances
npm install
# Lancer le serveur de développement
npm run dev
```

L'application est accessible sur `http://localhost:3000`.

## Configuration API

Par défaut, l'application se connecte à `http://127.0.0.1:8001`. Pour modifier l'URL de l'API, créer un fichier `.env.local` :

```
NEXT_PUBLIC_API_URL=http://votre-api.com
```

