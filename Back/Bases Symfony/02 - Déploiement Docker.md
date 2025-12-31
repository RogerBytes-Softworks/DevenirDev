# Déploiement Docker

Dans cette documentation, nous allons créer un projet Symfony et le déployer dans une pile de conteneurs Docker.
Ceci est basé [la doc de Symfony sur Docker](https://symfony.com/doc/current/setup/docker.html), [la doc d'install de Symfony](https://symfony.com/download) ainsi que [cette vidéo de Devscast](https://www.youtube.com/watch?v=dBjOBV64bIg).

## Création d'un nouveau projet Symfony

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On va verifier la dernière version LTS en date [sur le calendrier officiel](https://symfony.com/releases#symfony-releases-calendar) via cette commande :

```bash
curl -s https://symfony.com/releases \
  | grep 'Latest stable version' \
  | head -1 \
  | sed -E 's/.*Latest stable version: ([0-9]+\.[0-9]+\.[0-9]+)\. Latest LTS version: ([0-9]+\.[0-9]+\.[0-9]+).*/Stable: \1, LTS: \2/'
```

Il retourne `7.4.3` pour la LTS : l'on pourra donc passer l'argument `--version="7.4.*"` ou ` --version=lts` juste après.

On définit un nom de projet

```bash
PROJECT_NAME="test_symfony"
```

On se met dans le répertoire où l'on souhaite créer le projet, puis

```bash
symfony new $PROJECT_NAME --webapp --version=lts
cd $PROJECT_NAME
```

Cela a créé le projet complet (et déplacé à l'intérieur), pour faire une version "skeleton", il vous suffit de retirer l'argument `--webapp` de la commande.

  </div>
</details>

### Installer Php

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On installe Php en suivant [doc d'install de PHP](https://www.php.net/downloads.php?usage=web&os=linux&osvariant=linux-ubuntu&version=8.5).

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php -y
sudo apt update
```

On choisit d'installer `php 8.5`.

```bash
sudo apt install -y php8.5
```

Et on installe quelques paquets php

```bash
sudo nala install -y php8.5-cli php8.5-common php8.5-xml php8.5-mbstring php8.5-intl php8.5-sqlite3 php8.5-mysql php8.5-pgsql
```

Et on choisis la version utilisée par le système

```bash
sudo update-alternatives --config php
```

  </div>
</details>

### Installer Composer

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On installe la dernière version de Composer ([doc d'install de composer](https://getcomposer.org/download/))

```bash
php -r "copy('https://getcomposer.org/installer','composer-setup.php');" && \
php -r "copy('https://composer.github.io/installer.sig','sig');" && \
[ "$(php -r "echo hash_file('sha384','composer-setup.php');")" = "$(cat sig)" ] && \
php composer-setup.php --quiet && rm composer-setup.php sig || \
{ echo 'ERROR: Invalid installer checksum' >&2; rm composer-setup.php sig; exit 1; }
sudo mv composer.phar /usr/local/bin/composer
```

Pour désinstaller composer

```bash
sudo rm /usr/local/bin/composer
```

  </div>
</details>

## Installation

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On peut enfin lancer l'installation de Symfony :

```bash
wget https://get.symfony.com/cli/installer -O - | bash
sudo mv /home/$USER/.symfony5/bin/symfony /usr/local/bin/symfony
```

Le `sudo mv` ci-dessus est optionnel, mais il permet un accès global à l'executable.

On peut forcer Symfony à utiliser une version particulière de php, on affiche quel est le php système :

```bash
symfony local:php:list
```

Ici le système utilise `bin/php8.5`, donc on a l'imposer à Symfony.

```bash
echo 8.5 > ~/.php-version
```

On termine en vérifiant que nous ayons tous les outils et dépendances prérequis.

```bash
symfony check:requirements
```

Tout devrait être en vert, sinon résolvez les erreurs ou les recommendations.

  </div>
</details>

<style>
.spoiler {
  border-left: 4px solid #1abc9c;
  border-bottom-left-radius:3px;
  padding-left:10px;
  padding-top:15px;
  margin-top:-10px;
  margin-bottom:15px;
}
.button {
  cursor:pointer;
  padding:5px 10px;
  background-color:#3498db;
  color:white;
  border-radius:3px;
  margin-bottom:5px;
  display:inline-block;
  transition: background-color 0.2s;
}
.button:hover {
  background-color: #217dbb;
}
details[open] .button {
  background-color: #1abc9c;
}
</style>
