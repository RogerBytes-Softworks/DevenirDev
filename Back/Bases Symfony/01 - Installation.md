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

### Utilisation avec Docker

Il n'y a pas besoin d'utiliser un conteneur basé sur image de symfony, en revanche vous aurez besoin d'installer composer dans votre conteneur.

## Installer composer sur Docker

Aller dans le serveur apache (**attention le dockerfile doit importer PHP**)

Dans un shell il faut aller dans le container de docker.

```bash
docker exec -it NOM_DU_CONTENEUR bash
```

Prenons l'exemple avec un conteneur `serverApache851`.

```bash
docker exec -it serverApache851 bash
```

Ensuite :

installer les dépendances :

```bash
apt install -y nala
nala update
nala install -y zip unzip 7zip libzip-dev && docker-php-ext-install zip
```

Puis depuis [La Page officielle](https://getcomposer.org/download/) (attention la longue string change à chaque version) :

```bash
cd
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'c8b085408188070d5f52bcfe4ecfbee5f727afa458b2573b8eaaf77b3419b0bf2768dc67c86944da1544f06fa544fd47') { echo 'Installer verified'.PHP_EOL; } else { echo 'Installer corrupt'.PHP_EOL; unlink('composer-setup.php'); exit(1); }"
php composer-setup.php
php -r "unlink('composer-setup.php');"
mv composer.phar /usr/local/bin/composer
```

En production il est conseillé de supprimer composer une fois toutes les dépendances installées sur le conteneur, toujours en étant connecté dans son conteneur :

```bash
rm /usr/local/bin/composer
```

## Optional requirements

quand on fait

```bash
symfony check:requirements
```

regarder la ligne

```bash
> PHP is using the following php.ini file:
/etc/php/8.3/cli/php.ini
```

8.3 donne la version de php à utiliser, il faut intstaller

```bash
sudo nala install -y php8.3-intl
```

en précisant "php8.3-intl" la bonne version de phpo, ici j'ai mis 8.3

il di aussi

"

- "post_max_size" should be greater than "upload_max_filesize".
  > Set "post_max_size" to be greater than "upload_max_filesize".
  > "

donc

```bash
sudo nano /etc/php/8.3/cli/php.ini
```

chercher

`post_max_size`

et remplacer la valeur de 64 par 128
et enregistrer.
