# Installation de Symfony

En me basant [sur la doc de symfony](https://symfony.com/doc/current/setup.html) ainsi que [la doc d'installation](https://symfony.com/download).

## Installation CLI

```bash
wget https://get.symfony.com/cli/installer -O - | bash
```

On vérifie que nous avons tous les outils et dépendances prérequis.

```bash
symfony check:requirements
```

### Installer Php

On installe la dernière version de Php ([doc d'install de PHP 8.5](https://www.php.net/downloads.php?usage=web&os=linux&osvariant=linux-ubuntu&version=8.5))

```bash
sudo apt update
sudo apt install -y software-properties-common
sudo LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php -y
sudo apt update
sudo apt install -y php8.5
```

Et on choisis la version de php (plusieurs versions cohabitent, le php pré-installé par défaut n'est pas toujours à jour).

```bash
sudo update-alternatives --config php
```

### Installer Composer

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
