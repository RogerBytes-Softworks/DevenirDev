# Flexbox et Grid

## Préambule

Pour vous remettre aux sélecteur CSS, je recommande d'utiliser [CSS Diner](https://flukeout.github.io/) en premier lieu. Pour de la 3D il y a [Unfold](https://rupl.github.io/unfold/)(à faire après grid garden) et CSS Battle.

## Introduction

Ces deux outils sont très pratiques dans le cadre de l'affichage, grid permet de créer une espèce de découpage en tableau d'une boite, et Flexbox permet de déplacer les éléments dans une boîte.

Ces deux outils CSS sont indépendants mais peuvent être complémentaires.
Il n'est pas rare qu'ils soient utilisés conjointement, notamment en utilisant flexbox à l'intérieur de grid (le cas inverse n'existant pas à ma connaissance).

## Supports éducatifs

### Supports Flexbox

- [MDN Flexbox](https://developer.mozilla.org/fr/docs/Learn_web_development/Core/CSS_layout/Flexbox)
- [CSS Flexbox Layout Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Froggy](https://flexboxfroggy.com/#fr)
- [Flexbox Zombies](https://flexboxzombies.com/)

### Supports Grid

- [MDN Grid](https://developer.mozilla.org/fr/docs/Web/CSS/Guides/Grid_layout)
- [Grid Garden](https://cssgridgarden.com/#fr)
- [Outil de test Grid Playground](https://michalgrochowski.github.io/grid-playground/dist/)
- [cours freecodecamp](https://www.freecodecamp.org/news/heres-my-free-css-grid-course-merry-christmas-3826dd24f098/)
-

## Flexbox

Pour utiliser cette fonction CSS, sur chacun j'ai laissé la valeur par défaut.

On applique ce display sur un conteneur de la sorte

```css
.conteneur {
  display: flex; /* active Flexbox */
}
```

### Direction

Permet de changer les row en column, et au passage il permet de les inverser.

```css
flex-direction: row;
```

Attention, si l'on change l'axe des éléments d'une boîte élément avec `flex-directions`, `align-items` et `justify-content` ont leur rôles intervertis.

### Alignement horizontal du contenu d'une boîte

```css
justify-self: flex-start;
```

### Alignement vertical du contenu d'une boîte

```css
align-items: flex-start;
```

### Ordination d'un élément

Permet de changer l'ordre de l'élément dans sa boîte, fonctionne comme une array avec une indexation qui commence à zéro (l'index peut être également négatif tout comme une array).

```css
order: 0;
```

### Alignement horizontal d'un élément

**Cela n'existe pas, car il faut passer par du margin-left/right en auto, ou via l'ordre du conteneur !**

### Alignement vertical d'un élément

Permet de forcer l'alignement d'un élément en faisant fi de l'alignement donné au contenu de la boîte parente

```css
align-self: flex-start;
```

### Overflow et étalage sur une nouvelle row

De base dans quand on utilise `display: flex`, il y a `flex-shrink` qui essaye d'éviter l'overflow en rétrécissant la taille des éléments du conteneur (si la hauteur ou la largeur minimal sont atteints, notamment en auto pour son contenu), en gros vos éléments vont rétrécir tant qu'il n'auront pas à provoquer un overflow de leur propre contenu (en auto) ou si leur taille minimal est atteinte.

Une solution consiste à utiliser la fonction `wrap`. Permettant ainsi l'étalage sur une nouvelle row dès que les éléments du conteneur commencent à être trop serrés sur leur axe (si la direction est sur X, cela se met sur une nouvelle row, si c'est sur Y, une nouvelle colonne).

```css
flex-wrap: wrap; /* il faut mettre la valeur wrap pour l'activer */
```

On peut combiner `flex-direction` et `flex-wrap`

```css
flex-flow: column wrap; /* la première variable pour la direction, et la seconde pour l'étalage */
```
