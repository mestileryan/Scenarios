# Scénarios JDR

Recueil de scénarios de jeu de rôle sur table, mis en page pour le meneur de jeu :
thème sombre lisible dans le noir, système agnostique, narratif d'abord.

🌐 **Site publié** : une fois GitHub Pages activé, le recueil est consultable en ligne (voir ci-dessous).

## Structure

```
.
├── index.html              # Page d'accueil — liste les scénarios sous forme de cartes
├── scenarios/
│   └── <slug>/
│       └── index.html      # Un scénario mis en page
├── .github/workflows/
│   └── deploy.yml          # Déploiement automatique sur GitHub Pages
└── .claude/skills/
    └── jdr-scenario/       # Skill Claude Code qui génère les scénarios
```

## Créer un scénario

Donnez votre texte brut à Claude Code dans ce repo et demandez-lui de **créer un scénario**.
Le skill [`jdr-scenario`](.claude/skills/jdr-scenario/SKILL.md) s'occupe de tout :

1. il met en page le scénario dans `scenarios/<slug>/index.html` ;
2. il ajoute automatiquement une carte sur la page d'accueil (`index.html`).

Il n'y a rien à éditer à la main.

## Publication (GitHub Pages)

Le workflow [`deploy.yml`](.github/workflows/deploy.yml) publie le site à chaque push sur `main`
(ou `master`). Pour l'activer **une seule fois** :

1. GitHub → **Settings** → **Pages**
2. **Build and deployment** → **Source** : choisir **GitHub Actions**

Le site sera alors disponible à l'adresse
`https://<utilisateur>.github.io/<nom-du-repo>/`.

## Aperçu en local

Comme tout est en fichiers statiques, ouvrez simplement `index.html` dans un navigateur,
ou servez le dossier :

```bash
python -m http.server 8000
# puis http://localhost:8000
```
