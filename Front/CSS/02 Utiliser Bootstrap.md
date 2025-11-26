# Utilisation de Bootstrap

## Ajouter Bootstrap à un projet

Pour installer BootStrap l'on peut passer par le CDN (une connexion au site de bootstrap) ou via npm, un gestionnaire de paquet node.js (qui permet de le télécharger dans votre projet).

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
  src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"
  integrity="sha384-FKyoEForCGlyvwx9Hj09JcYn3nv7wiPVlz7YYwJrWVcXK/BmnVDxM+D2scQbITxI"
  crossorigin="anonymous"
></script>
```

### Installer avec NPM

```bash
npm install bootstrap@5.3.8
```

Il faut l'installer à la racine de votre projet git et ensuite le mettre dans votre `HEAD`

```html
<link
  href="./node_modules/bootstrap/dist/css/bootstrap.min.css"
  rel="stylesheet"
/>
```

et juste avant votre fermeture `<\body>` copiez

```html
<script src="./node_modules/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
```

Si vous l'utilisez dans un projet côté serveur, du genre avec un environnement node.js suivez les indications [depuis cette page](https://getbootstrap.com/docs/5.3/getting-started/download/#package-managers).

## Utilisation de BootStrap

### Extensions Codium

Depuis le marketplace avec mon petit programme `vsix-dl`

```bash
vsix-dl AnbuselvanRocky.bootstrap5-vscode
vsix-dl hossaini.bootstrap-intellisense
vsix-dl HansUXdev.bootstrap5-snippets
```

Je créé un index

```bash
touch index.html
```

et à l'intérieur j'utilise le snippet natif `!` (qui utilise la dernière version de html) et je lance live server via `clic droit` + `Open with Live Server`, le lien à utiliser est

```https
http://127.0.0.1:5500/
```

[Lien du tuto](https://www.youtube.com/watch?v=MTRHi0gxPEo)
