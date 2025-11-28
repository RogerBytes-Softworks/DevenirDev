# Bootstrap

## Ajouter Bootstrap à un projet

Pour installer Bootstrap on peut passer par le CDN (une connexion au site de Bootstrap) ou via npm, un gestionnaire de paquets Node.js (qui l'installe dans votre projet).

Les instructions suivantes proviennent [de la page dédiée bootstrap](https://getbootstrap.com/), vérifiez qu'elles soient à jour.

### Utiliser le CDN

Incluez-le dans votre `<head>`.

```html
<link
  href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css"
  rel="stylesheet"
  integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB"
  crossorigin="anonymous"
/>
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
      border: 1px dashed darkblue;
    }
  </style>

  <div class="container">
    <div class="row text-center justify-content-center">
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

Et si on ne souhaite pas faire de breakpoint (en gros le même affichage peu importe le support) on peut également définir un nombre de colonne par défaut par ligne (pour des colonnes avec la même taille) avec `row-cols-` suivi du nombre de colonnes désirées.

```html
<body>
  <style>
    .container,
    .row div {
      background-color: aqua;
      border: 1px dashed darkblue;
    }
  </style>

  <div class="container">
    <div class="row text-center justify-content-center row-cols-3">
      <div class="col">col 1</div>
      <div class="col">col 2</div>
      <div class="col">col 3</div>
      <div class="col">col 4</div>
    </div>
  </div>
</body>
```

On utilise `col` comme classe pour chaque élément, ici nous avons donc trois colonnes par ligne. Attention, si l'on donne une largeur à `col-` à unj ou des éléments, ça prend le dessus sur `row-cols-` sur la ligne modifiée.

On remarque aussi que j'ai utilisé `justify-content-center` dans mon exemple, il s'agit du fonctionnement de flex, donc l'on peut utiliser ses variantes :

On remarque aussi que j'ai utilisé `justify-content-center` dans mon exemple, (il s'agit bien de Flexbox derrière Bootstrap), donc l'on peut utiliser ses variantes :

- `justify-content-start` → aligne les éléments au début de la ligne (à gauche en LTR)
- `justify-content-end` → aligne les éléments à la fin de la ligne (à droite en LTR)
- `justify-content-center` → centre les éléments horizontalement
- `justify-content-between` → espace les éléments pour qu’il y ait le maximum d’espace entre eux
- `justify-content-around` → espace les éléments avec un espace égal autour de chaque élément
- `justify-content-evenly` → espace les éléments avec un espacement égal entre eux et aux extrémités

Pareil pour `align-items` et `align-self` (voir documentation de Flexbox).

Il est aussi parfaitement possible de faire du nesting (de l'imbrication), à l'intérieur des cellules d'un grid Bootstrap, le fonctionnement est similaire à du Grid classique, voici un exemple :

```html
<style>
  .container,
  .row div {
    background-color: aqua;
    border: 1px dashed darkblue;
  }
</style>

<div class="container">
  <div class="row text-center justify-content-center">
    <div class="col-12 col-md-6 col-lg-4">col 1</div>
    <div class="col-12 col-md-6 col-lg-4">col 2</div>
    <div class="col-12 col-md-6 col-lg-4">col 3</div>
    <div class="col-12 col-md-6 col-lg-4">
      <div class="row row-cols-2">
        <div class="col bg-success">nested 1 in col 4</div>
        <div class="col bg-warning">nested 2 in col 4</div>
      </div>
    </div>
  </div>
</div>
```

### Utilisation du margin et du padding

- **Padding** : c’est l’espace **à l’intérieur** d’un élément, entre le contenu et sa bordure. Exemple : `padding: 10px`, le texte ne touchera pas directement les bords du div.
- **Margin** : c’est l’espace **à l’extérieur** d’un élément, entre cet élément et les autres éléments autour. Exemple : `margin: 10px` éloigne le div de ses voisins.

En Bootstrap, il y a des classes pratiques pour les deux :

- `p-1` à `p-5` → padding sur tous les côtés
- `pt-1` → padding-top, `pb-2` → padding-bottom, etc.
- `m-1` à `m-5` → margin sur tous les côtés
- `mt-2` → margin-top, `mx-3` → margin horizontal, `my-4` → margin vertical

On peut aussi utiliser `px-` et `py-` pour le paddings, ainsi que `m-` et `p-` si la marge et le pad sont identiques sur les axes x et y.

Représentation simplifiée :

```text
Margin
┌───────────────────────────┐
│ Border                    |
│ ┌───────────────────────┐ |
│ │ Padding               | |
│ │ ┌───────────────────┐ │ |
│ │ │     Content       │ │ |
│ │ └───────────────────┘ │ |
│ └───────────────────────┘ |
└───────────────────────────┘
```

Explications :

- **Content** : le texte, image ou élément à l'intérieur du div.
- **Padding** : espace entre le contenu et la bordure du div.
- **Border** : la bordure du div (optionnelle).
- **Margin** : espace entre ce div et les autres éléments autour.

Par exemple, en reprenant une grid Bootstrap

```html
<style>
  .container,
  .row div {
    background-color: aqua;
    border: 1px dashed darkblue;
  }
</style>

<div class="container">
  <div
    class="row text-center justify-content-center row-cols-2 p-5 m-2 bg-danger"
  >
    <div class="col bg-primary text-light">nested</div>
    <div class="col bg-secondary text-light">nested</div>
  </div>

  <div class="row text-center justify-content-center">
    <div class="col-12 col-md-6 col-lg-4">col 1</div>
    <div class="col-12 col-md-6 col-lg-4">col 2</div>
    <div class="col-12 col-md-6 col-lg-4">col 3</div>
    <div class="col-12 col-md-6 col-lg-4">
      <div class="row row-cols-2 bg-primary pt-2 pb-5 mx-2 my-3">
        <div class="col bg-success">nested 1 in col 4</div>
        <div class="col bg-warning">nested 2 in col 4</div>
      </div>
    </div>
  </div>
</div>
```

On voit (via live server) assez nettement les marges et les pad avec les différentes couleurs.

### Mettre du gap entre les colonnes

Au niveau de la classe, c'est pareil que pour le margin et le padding, mais avec la lettre `g`.

```html
<style>
  .container,
  .row div {
    background-color: aqua;
    border: 1px dashed darkblue;
  }
</style>

<div class="container">
  <div class="row text-center justify-content-center my-3 gx-2 gy-1 bg-danger">
    <div class="col-10 col-md-5 col-lg-3 bg-primary text-light">nested</div>
    <div class="col-10 col-md-5 col-lg-3 bg-secondary text-light">nested</div>
  </div>

  <div class="row text-center justify-content-center g-2 bg-secondary">
    <div class="col-10 col-md-5 col-lg-2">col 1</div>
    <div class="col-10 col-md-5 col-lg-2">col 2</div>
    <div class="col-10 col-md-5 col-lg-2">col 3</div>
    <div class="col-10 col-md-5 col-lg-2">
      <div class="row row-cols-2 bg-primary pt-2 pb-5 mx-2 my-3">
        <div class="col bg-success">nested 1 in col 4</div>
        <div class="col bg-warning">nested 2 in col 4</div>
      </div>
    </div>
  </div>
</div>
```

Attention, il faut faire attention à ce que les colonnes ne s'étalent pas sur l’entièreté du display de la grid avant d'ajouter un gap, sinon ça provoque un overflow !
Il vaut mieux une grid avec des colonnes bien réglées que de tricher en mettant la classe Bootstrap `overflow-hidden` sur le conteneur.

### Utiliser des components Bootstrap

Les composants Bootstrap sont des éléments préconçus (boutons, cartes, alertes, modals…) que l’on peut directement intégrer dans sa page pour gagner du temps et conserver une cohérence visuelle.

Les components (ou composants dans la langue de Molière) sont disponible dans la nav latérale de [la page "Docs" du site](https://getbootstrap.com/docs/5.3/getting-started/introduction/), c'est sur ces pages que j'ai pris les exemples qui vont suivre, il y a plein d'éléments prêts à être utilisés sur la documentation officielle de Bootstrap.

#### Boutons

Voici des exemples de [boutons](https://getbootstrap.com/docs/5.3/components/buttons/).

```md
<button type="button" class="btn btn-primary">Primary</button>
<button type="button" class="btn btn-secondary">Secondary</button>
<button type="button" class="btn btn-success">Success</button>
<button type="button" class="btn btn-danger">Danger</button>
<button type="button" class="btn btn-warning">Warning</button>
<button type="button" class="btn btn-info">Info</button>
<button type="button" class="btn btn-light">Light</button>
<button type="button" class="btn btn-dark">Dark</button>

<button type="button" class="btn btn-link">Link</button>
```

On peut assigner les classes de boutons à d'autres éléments

```md
<a class="btn btn-primary" href="#" role="button">Link</a>
<a class="btn btn-outline-primary" href="#" role="button">Link outline</a>
<button class="btn btn-primary" type="submit">Button</button>
<input class="btn btn-primary" type="button" value="Input">
<input class="btn btn-primary" type="submit" value="Submit">
<input class="btn btn-primary" type="reset" value="Reset">
```

#### Modales

Voici des exemples de [modales](https://getbootstrap.com/docs/5.3/components/modal/).

Ici je vais me servir du snippet (grâce aux extensions) `bs5-modal-toggle`, il va me copier tout le bloc nécessaire.
