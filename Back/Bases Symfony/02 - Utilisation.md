# Installation de Symfony

En me basant [sur la doc de Symfony](https://symfony.com/doc/current/setup.html) ainsi que [la doc d'installation](https://symfony.com/download).

## Dépendances

Il faut installer `PHP` puis `Composer`.

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
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'c8b085408188070d5f52bcfe4ecfbee5f727afa458b2573b8eaaf77b3419b0bf2768dc67c86944da1544f06fa544fd47') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }"
php composer-setup.php
php -r "unlink('composer-setup.php');"
sudo mv composer.phar /usr/local/bin/composer
```

Pour désinstaller composer

```bash
sudo rm /usr/local/bin/composer
```

Pour le mettre à jour

```bash
composer self-update
```

  </div>
</details>

## Installation

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

```bash
wget https://get.symfony.com/cli/installer -O - | bash
sudo mv /home/$USER/.symfony5/bin/symfony /usr/local/bin/symfony
```

On peut forcer Symfony à utiliser une version particulière de php

```bash
symfony local:php:list
```

```bash
echo 8.5 > ~/.php-version
```

On termine en vérifiant que nous ayons tous les outils et dépendances prérequis.

```bash
symfony check:requirements
```

  </div>
</details>

## Docker et Symfony

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

Dans le répertoire `stack` j'ai préparé un composer et des dockerfiles permettant d'avoir une stack compatible et fonctionnelle avec Symfony.



```bash
docker exec -it NOM_DU_CONTENEUR bash
```

Prenons l'exemple avec un conteneur `serverApache851`.

```bash
docker exec -it serverApache851 bash
```

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

/* hover classique */
.button:hover {
  background-color: #217dbb;
}

/* bouton quand le spoiler est ouvert */
details[open] .button {
  background-color: #1abc9c;
}
</style>
