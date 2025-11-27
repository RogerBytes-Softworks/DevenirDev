# Bootstrap

## Ajouter Bootstrap à un projet

Pour installer Bootstrap on peut passer par le CDN (une connexion au site de Bootstrap) ou via npm, un gestionnaire de paquets Node.js (qui l'installe dans votre projet).

Les instructions suivantes proviennent [de la page dédiée bootstrap](https://getbootstrap.com/), vérifiez qu'elles soient à jour.

### Utiliser le CDN

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
  rel="stylesheet"
  integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB"
  crossorigin="anonymous"
/>
```

et à la fin, juste avant `</body>`

```html
<script
  defer
  src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"
  integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI"
  crossorigin="anonymous"
></script>
```

Le defer est recommandé afin de ne pas bloquer le rendu quand le script se charge.

### Installer avec NPM

```bash
npm install bootstrap@5.3.8
```

Installez-le à la racine de votre projet git, puis incluez-le dans votre `<head>`.

```html
<link
  href="./node_modules/bootstrap/dist/css/bootstrap.min.css"
  rel="stylesheet"
/>
```

et juste avant votre fermeture `</body>` collez

```html
<script
  defer
  src="./node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"
></script>
```

Si vous l'utilisez dans un projet côté serveur, du genre avec un environnement node.js suivez les indications [depuis cette page](https://getbootstrap.com/docs/5.3/getting-started/download/#package-managers).

## Utilisation de Bootstrap

Pour rédiger ce qui suit, j'ai suivi [ce tutoriel vidéo](https://www.youtube.com/watch?v=MTRHi0gxPEo).

### Extensions Codium

Depuis le marketplace avec mon petit programme `vsix-dl` conçu pour VSCodium (pour les extensions disponibles seulement pour VSCode), je lance l'installation via :

```bash
vsix-dl AnbuselvanRocky.Bootstrap5-vscode
vsix-dl hossaini.Bootstrap-intellisense
vsix-dl HansUXdev.Bootstrap5-snippets
```

Cela permet d'installer `Bootstrap 5 Quick Snippets`, `Bootstrap IntelliSense` et `Bootstrap 5 & Font Awesome Snippets`.

### Initialisation du projet

Je crée un index

```bash
touch index.html
```

et à l'intérieur j'utilise le snippet natif `!` (qui utilise la dernière version de html) et je lance live server via `clic droit` + `Open with Live Server`,  le lien généré par Live Server est

```https
http://127.0.0.1:5500/
```

## Balisage et couleurs

Voici les balises html textuelles habituelles, pour rappel.

```html
<p>Texte <mark>surligné</mark></p>
<p>Texte <del>supprimé</del></p>
<p>Texte <s>dépassé et barré</s></p>
<p>Texte <ins>Ajouté au document</ins></p>
<p>Texte <u>souligné</u></p>
<p>Texte <small>en petits caractères</small></p>
<p>Texte <strong>mis en évidence en gras</strong></p>
<p>Texte <em>mis en italique</em></p>
```

On peut changer la couleur du texte via des classes BS.

```html
<p class="text-primary">.text-primary en bleu</p>
<p class="text-secondary">.text-secondary en gris</p>
<p class="text-success">.text-success en vert</p>
<p class="text-danger">.text-danger en rouge</p>
<p class="text-warning">.text-warning en jaune</p>
<p class="text-info">.text-info en bleu ciel</p>
<p class="text-light bg-secondary">.text-light en gris clair</p>
<p class="text-dark bg-secondary">.text-dark en noir</p>
<p class="text-muted">.text-muted en gris, utile pour les liens désactivés</p>
<p class="text-white bg-secondary">.text-white en blanc</p>
```

Les couleurs de Bootstrap sont `primary`, `secondary`, `success`, `danger`, `warning`, `info`, `light`, `dark`, `muted` et `white`.

## Les breakpoints

Les _breakpoints_ sont des largeurs personnalisables qui déterminent comment votre mise en page responsive se comporte selon la taille de l’appareil ou de la fenêtre dans Bootstrap.

Pour faire simple, les valeurs à utiliser pour du responsive sont

- Vue téléphone : la classe "extra small" pour du <576px, pas besoin de la préciser: c'est ce qu'il y a par défaut
- Vue tablette : la classe "medium" `md` pour du ≥768px, dispensable (souvent tablette et desktop ont la le même rendu)
- Vue desktop : la classe "large" `lg` pour du ≥992px,

C'est en réalité une media query interne à Bootstrap.

Voici un exemple de code permettant de comprendre le breakpoint

```html
<style>
  .container-fluid {
    background-color: aqua;
    border: 1px darkblue;
  }
</style>

<div class="container-fluid">Container</div>
```

Si vous remplacez `container-fluid` par `container` vous verrez alors qu'en étirant en largeur, le container ne s'étalera plus à 100% du viewport passé une certaine largeur.

`fluid` est une valeur spéciale de breakpoint, indiquant de s'étendre à 100% tout le temps.

## La grille Bootstrap

Bootstrap utilise un système de grille inspiré du CSS Grid, basé sur un layout de 12 colonnes par ligne (`row`).

- Si vous utilisez des classes `col-{nombre}`, la somme des colonnes est limitée à 12 par ligne, et les colonnes excédentaires passent à la ligne suivante.
- Si vous utilisez simplement `col`, chaque colonne prend une part égale de l’espace disponible, et vous pouvez avoir plus de 12 colonnes sur une seule ligne si la largeur le permet.

on utilise `.row` et `.col` pour générer les row et les columns.

```html
<body>
  <style>
    .container,
    .row div {
      background-color: aqua;
      border: 1px dashed red;
    }
  </style>

  <div class="container">
    <div class="row text-center">
      <div class="col-3">col 3</div>
      <div class="col-3">col</div>
      <div class="col-3">col</div>
      <div class="col-3">col</div>
    </div>
  </div>
</body>
```

(le style inline est acceptable pour le tuto, dans un vrai projet on importe un fichier css dans le `<head>`)

Ici, il y a 4 colonnes de 3/12 de largeur, elles s’étirent donc correctement.
Si vous ajoutez une colonne supplémentaire ou modifiez une colonne en col-4 de façon à dépasser 12, elle ira automatiquement à la ligne suivante.

Pour que vos lignes s’étendent proprement avec les colonnes, il est recommandé que la somme des tailles fasse 12 colonnes.

### Breakpoint dans une grid Bootstrap

Si l'on commence à faire notre site en "mobile-first" (c'est à dire la version portrait et plus petite en premier, ce qui est recommandé).

Donc pour le mobile on utilise simplement `col-` (on ne précise pas, on est en "extra small" par défaut), pour la tablette on utilise `col-md-` et pour la vue desktop on se sert de `col-lg-`.

Mis en pratique cela donne ceci :

```html
<body>
  <style>
    .container,
    .row div {
      background-color: aqua;
      border: 1px dashed red;
    }
  </style>

  <div class="container">
    <div class="row text-center justify-content">
      <div class="col-12 col-md-6 col-lg-4">col 1</div>
      <div class="col-12 col-md-6 col-lg-4">col 2</div>
      <div class="col-12 col-md-6 col-lg-4">col 3</div>
      <div class="col-12 col-md-6 col-lg-4">col 4</div>
    </div>
  </div>
</body>
```

Chaque breakpoint remplace le précédent dès que la largeur devient suffisante, si une classe existe (comme ici, il y a `xs`, `md` et `lg`).

Explication :

- `col-12` en vue mobile "extra small" (on n'écrit pas "xs" c'est mis par défaut) étend l'élément sur l'ensemble du layout (de douze colonnes), donc un élément par ligne en mobile
- `col-md-6` en vue tablet "medium" étend l'élément sur 6/12e du layout, donc deux éléments par ligne en tablet
- `col-lg-4` en vue desktop "large" étend l'élément sur 4/12e du layout, donc trois éléments par ligne en desktop
