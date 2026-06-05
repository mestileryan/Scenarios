# Composants — aide-mémoire

Tous les composants existent déjà dans `assets/template.html`. Copie le bloc voulu et remplace le contenu. Ne réécris jamais le CSS : il est complet.

## 1. Callouts (encadrés)
Trois variantes, structure identique (icône SVG + `c-title` + `<p>`). Seule la classe change.

- **À lire à voix haute** → `<div class="callout read">` — fond parchemin doré, texte en italique serif. Pour tout ce que le MJ narre mot pour mot aux joueurs. Mets le texte entre guillemets « ».
- **Info MJ** → `<div class="callout gm">` — bleu. Conseils de coulisses, rythme, adaptation.
- **Danger / attention** → `<div class="callout warn">` — rouge. Menaces, pièges, conséquences.

Garde les icônes SVG telles quelles (volume pour `read`, cercle-i pour `gm`, triangle pour `warn`).

## 2. Pastilles d'épreuve (difficulté en mots)
Système agnostique, sans chiffres. Quatre niveaux, couleur + jauge à 3 points :

```html
<span class="epreuve facile"><span class="gauge"><i></i><i></i><i></i></span>Facile</span>
<span class="epreuve modere"><span class="gauge"><i></i><i></i><i></i></span>Modéré</span>
<span class="epreuve difficile"><span class="gauge"><i></i><i></i><i></i></span>Difficile</span>
<span class="epreuve tres-difficile"><span class="gauge"><i></i><i></i><i></i></span>Très difficile</span>
```

Règles : toujours 3 `<i>` dans la jauge (le remplissage est géré en CSS par la classe). `tres-difficile` est réservé aux moments d'exception. S'utilise en ligne dans une phrase ou en fin de puce d'action. La légende complète va dans la section « Échelle de difficulté » de l'intro.

## 3. Déroulants `<details>`
Deux usages, même squelette (chevron SVG + libellé + `<span class="tag">`).

- **Fiche PNJ** → `<details>` + `<div class="details-body pnj">`. Format narratif, jamais de stats chiffrées. Lignes typiques : *Ce qu'il veut · Ce qu'il cache · Sa voix · Levier dramatique*. La ligne « Sa voix » utilise `class="v p-voice"` (italique serif) pour aider à incarner le personnage.
- **Secret** → `<details class="secret">`. Pour les révélations que les joueurs ne doivent pas voir tout de suite. Le libellé du `summary` doit signaler quand l'ouvrir (ex. « — ne pas révéler tout de suite »).

## 4. Sommaire (sidebar)
Un `<a href="#id">` par section ou scène. Les liens principaux portent `<span class="dot"></span>` ; les sous-éléments ajoutent `class="sub"`. Chaque `href` doit pointer vers l'`id` d'une `<section>` ou d'un ancrage `<div id="...">` placé juste avant le `<h3>` de la scène. Le surlignage du lien actif est automatique (script en bas de page) — ne rien câbler à la main.

## 5. Tables aléatoires & récompenses
- Tables → `<table>` avec `<th>d6</th>` ; la première colonne (le chiffre) est colorée automatiquement.
- Récompenses → liste `<ul>`, décrites par leur effet de fiction, pas par des bonus chiffrés.

## Reskin rapide
Pour changer l'ambiance, modifie seulement `--accent` et `--accent-soft` dans `:root`, et éventuellement les deux `radial-gradient` du `body`. Le reste de la palette (sombre, lisible dans le noir) reste tel quel.
