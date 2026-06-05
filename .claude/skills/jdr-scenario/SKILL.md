---
name: jdr-scenario
description: >-
  Met en page un scénario de jeu de rôle sur table dans un fichier index.html
  autonome, sombre et responsive, pensé pour un MJ qui lit sur écran (y compris
  dans le noir). Utilise ce skill dès que l'utilisateur veut créer, mettre en
  forme ou exporter un scénario, une aventure, un one-shot, un module ou un
  document de MJ — en français comme en anglais, et même s'il ne dit pas
  explicitement « HTML » ou « mise en page ». Déclenche-le aussi quand la demande
  mentionne des encadrés « à lire à voix haute », des fiches de PNJ, des secrets à
  cacher, des actes/scènes, ou des niveaux de difficulté narratifs. Ne pas
  utiliser pour des fiches de personnage, des règles de système, ou des contenus
  non-JDR.
---

# Scénario JDR — format MJ

Génère un scénario de jeu de rôle dans un **seul fichier `index.html`** : thème sombre, responsive, sommaire latéral fixe, encadrés de lecture, pastilles de difficulté en mots, et blocs déroulants pour les PNJ et les secrets. Le but est un document qu'un meneur de jeu (MJ) lit confortablement en table, sur mobile comme sur ordinateur.

**Ce skill s'utilise dès que l'utilisateur demande de créer/mettre en forme un scénario.** Le travail part d'un **texte brut** (l'idée ou les notes de l'utilisateur) et produit un rendu mis en page **directement dans ce repo Git**, qui est publié via GitHub Pages. Le scénario va dans `scenarios/<slug>/index.html` et une carte est ajoutée à la page d'accueil `index.html` à la racine — pas de sortie vers `/mnt/...`.

## Principes de ce format

- **Système agnostique.** Aucune statistique chiffrée, aucun seuil de jet. La difficulté s'exprime en mots (Facile / Modéré / Difficile / Très difficile) que chaque table traduit dans son propre système.
- **Narratif d'abord.** Les PNJ sont décrits par leurs intentions et leur voix, pas par des caractéristiques. Le combat est une option parmi d'autres, jamais la valeur par défaut.
- **Lisible dans le noir.** Fond charbon (pas noir pur), texte chaud, contraste maîtrisé. Police Inter pour le corps (lisibilité maximale), serif Spectral pour les titres et les passages narrés.
- **Un seul fichier.** Tout le CSS est dans une balise `<style>`. Un court script gère uniquement le surlignage du lien actif et le menu mobile ; tout le reste fonctionne sans JavaScript.

## Procédure

1. **Pars du template.** Lis `assets/template.html` : il contient tout le CSS prêt à l'emploi et un squelette commenté avec un exemple de chaque composant. Copie-le et remplis-le ; ne réécris pas le CSS.
2. **Consulte les composants si besoin.** `references/components.md` est l'aide-mémoire : quel encadré utiliser, comment écrire une pastille de difficulté, comment structurer une fiche PNJ ou un secret.
3. **Structure le scénario** à partir du texte brut fourni, en Introduction → Actes (avec scènes) → Annexes. Donne un `id` à chaque `<section>` et un ancrage `<div id="...">` avant chaque scène, puis ajoute le lien correspondant dans le sommaire. Si l'utilisateur n'a pas de contenu précis, propose un scénario complet et cohérent.
4. **Remplis le contenu** : accroche, synopsis, notes MJ, scènes avec actions et difficultés, fiches PNJ, secrets, tables aléatoires, récompenses.
5. **Lien retour vers l'accueil.** Dans la sidebar du scénario, enveloppe le bloc `.brand` dans `<a href="../../" ...>` pour que le MJ revienne au recueil. (Le chemin `../../` part de `scenarios/<slug>/` vers la racine.)
6. **Choisis un slug** en kebab-case ASCII à partir du titre (minuscules, sans accents ni espaces ; ex. « Le Manoir des Murmures » → `le-manoir-des-murmures`).
7. **Enregistre le scénario** dans le repo : `scenarios/<slug>/index.html`.
8. **Mets à jour la page d'accueil** (`index.html` à la racine) — voir la section ci-dessous.
9. **Présente le résultat** : indique le chemin du scénario, la carte ajoutée, et rappelle que le site se publie tout seul au prochain push (GitHub Pages).

## Mettre à jour la page d'accueil

La racine du repo contient `index.html`, le recueil qui liste les scénarios sous forme de cartes. À chaque nouveau scénario :

1. Copie le gabarit `assets/card.html` et remplis-le (`{{SLUG}}`, `{{GENRE}}`, `{{FORMAT}}`, `{{TITRE}}`, `{{ACCROCHE}}`, `{{DUREE}}`, `{{NB_PJ}}`, `{{THEMES}}`). Le `href` doit être `scenarios/<slug>/`.
2. Insère la carte dans `index.html` **juste avant** le marqueur `<!-- SCENARIOS:END -->`.
3. **Première carte uniquement** : supprime le bloc `<div class="empty">…</div>` (l'état « aucun scénario ») situé entre les marqueurs.
4. Ne touche à rien d'autre dans `index.html` : la grille et le style sont déjà en place.

## Composants disponibles (détail dans references/components.md)

- **Callouts** : `read` (à lire à voix haute, doré), `gm` (info MJ, bleu), `warn` (danger, rouge).
- **Pastilles d'épreuve** : `facile`, `modere`, `difficile`, `tres-difficile`. Toujours 3 points dans la jauge ; le CSS gère le remplissage selon la classe.
- **Déroulants** : `<details>` + `.pnj` pour les fiches narratives, `<details class="secret">` pour ce qui se révèle plus tard.
- **Sommaire latéral** fixe avec surlignage automatique de la section en cours et repli en hamburger sur mobile.
- **Tables** aléatoires et listes de **récompenses** décrites par la fiction.

## Garde-fous

- Pas de valeurs chiffrées de jeu (PV, DD, bonus, CA). Si l'utilisateur en veut malgré tout, garde le format mais préviens que le skill vise le narratif universel, et propose une fiche PNJ narrative en parallèle.
- Le texte des callouts `read` est destiné à être lu tel quel aux joueurs : écris-le entre guillemets « », immersif, à la deuxième personne.
- Garde le contraste sombre. Pour reskiner, change uniquement `--accent` / `--accent-soft` et les dégradés du `body` ; ne passe pas en thème clair (ça défait l'objectif « lisible dans le noir »).
- Adapte la langue du document à celle de l'utilisateur.
