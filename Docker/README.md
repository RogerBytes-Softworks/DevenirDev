# Utilisation

## Prérequis

- git
- docker
- php

## Conception de ma pile de conteneurs Docker

Création de ma pile de container, depuis docker desktop, je recherche les images dans la barre de recherche en haut

- `dbeaver/cloudbeaver`
- `postgres`
- `node:lts-trixie-slim`

Vu que c'est un projet pédagogique, j'ai fusionné les deux piles que sont le front et le back, pour faire le front je n'aurais grosso modo que la partie node du compose.yml sans nécessité d'avoir de dockerfile (à vérifier).

### Port internes et externes

Le **port interne** est celui que l’application (CloudBeaver) écoute à l’intérieur du conteneur, ici `8978`. Le **port externe** est celui de votre machine locale qui redirige vers ce port interne, ici `7851`.

Quand on va sur `http://localhost:7851`, Docker fait passer le trafic vers le port `8978` à l’intérieur du conteneur. Sans cette redirection, tu ne pourrais pas accéder à l’application depuis ton navigateur.

### Sécurité de connexion avec un .env

Dans le `compose.yml`
Dans les variable d'environnement du service `web` j'ai ces variables :

```yml
- DB_USER=${DB_USER}
- DB_PASSWORD=${DB_PASSWORD}
```

et dans les variable d'environnement du service `postgres` j'ai ces variables :

```yml
- POSTGRES_PASSWORD=${DB_PASSWORD}
```

Implicitement `${DB_USER}` et `${DB_PASSWORD}` seront interprétés comme les variables d’environnement correspondantes dans le fichier `.env` sous cette forme (dans le cas présent, qui sert de projet pédagogique) :

```bash
cat <<EOF > .env
DB_USER="root"
DB_PASSWORD="root"
EOF
```

⚠️ **Évitez ABSOLUMENT** d'utiliser des identifiants sensibles (comme `root`) en clair dans un projet.

On ajoute ce fichier dans le .gitignore (en ajoutant une ligne `.env` dans le `.gitignore`) pour éviter de l’exposer dans un dépôt Git. Lors du déploiement, le `.env` est ensuite injecté via Docker (placé au même niveau que le `docker-compose.yml`), par exemple avec un outil d’intégration continue.

```bash
cat <<EOF > .gitignore
.env
EOF
```

### Déploiement local avec Docker

Présentement je ne vais pas détailler les fichiers `compose.yml` (qui génère les conteneurs) et `Dockerfile` (qui sert au compose via la directive `build`) afin de rendre la mise en place du projet plus rapide, ce sera détaillé quand le projet sera fini, en fin de documentation.

Déploiement :

```bash
docker compose up -d # Créé la pile de conteneurs
```

sur un serveur distant

```bash
ssh user@remote-server "cd /chemin/du/projet && docker compose up -d"
```

ça pourrait donner un truc du genre

```bash
ssh harry@192.168.1.42 "cd /home/harry/mon-projet && docker compose up -d"
```

Dans ce cas le chemin doit pointer vers l’endroit où vos fichiers (`docker-compose.yml`, `.env`, etc.) sont présents **sur le serveur distant**, pas sur votre machine locale.

Si jamais la pile est à supprimer pour la modifier

```bash
docker compose down -v
```

Il faut bien utiliser le `-v` dans la commande afin de bien effacer les anciens volumes.

Dans `compose.yml` on note que le chemin de node est dans le dossier `frontend` et pour la partie back ça se trouve dans `php-docker-app`

On va faire un `npm init` pour activer node.

```bash
cd ./frontend
npm init -y
echo 'console.log("Node fonctionne !");' > index.js
npm pkg set scripts.start="node index.js"
cd ../
```

Et pour le back dans `php-docker-app`

```bash
volume_path=php-docker-app
[ ! -f "$volume_path/index.php" ] && echo "<?php\necho 'Hello, World!';\n?>" > "$volume_path/index.php"
```

Ca génère le dossier `$volume_path` et également un fichier index.php avec un "Hello World" le projet est vierge.

## Démarrer l'application en local

On lance docker-desktop et le conteneur docker avec :

```sh
/opt/docker-desktop/bin/docker-desktop
```

Et

```bash
docker compose start        # Lancer les conteneurs
docker compose stop         # Stopper les conteneurs
```

Pour afficher dans le navigateur :

- [Connexion au projet sur le port 8851](http://localhost:8851/)
- [Connexion à cloudbeaver sur le port 7851](http://localhost:7851/)

Voici les différent port du `compose.yml`

- apache : 8851:80
- cloudbeaver : 7851:8978
- postgres : 3851:5432
- node : 8888:8888

### Setup CloudBeaver

J'au rempli **Administrator Credentials**.
**Login** : `Admin-user`
**Password** `Admin-password-1234`
**Repeat Password** `Admin-password-1234`

Normalement CloudBeaver est prêt à être utilisé, il ne reste qu'à cliquer sur son icone en haut à droite pour accéder au **tableau de bord CloudBeaver**..

### Connexion CloudBeaver

1. Dans le tableau de bord, cliquez sur **New Connection** et cherchez "PostgreSQL".
2. Créez une connexion PostgreSQL avec :

- **Host** : `postgres` (il s'agit du nom du service dans le .yml postgres:)
- **Port** : `5432` (le port "3851:5432")
- **Database** : `blog` (il s'agit de la valeur dans le .yml POSTGRES_DB=blog )
- **User name** : `root` (ce que j'ai stocké dans le .env dans notre cas)
- **User password** : `root` (ce que j'ai stocké dans le .env dans notre cas)

Après ça, vous pourrez explorer vos tables et données.

### Serveur

- Serveur = `postgres`
- Utilisateur = `root`
- Mot de passe = `root`

### Connexion en CLI

```bash
docker exec -it <nom_du_conteneur> /bin/bash
```

donc dans le cas présent, pour le conteneur postgres de la pile

```bash
docker exec -it serverPostgres851 /bin/bash
```

Dans les conteneur, il y a :

- serverApache851
- serverPostgres851
- serverCloudBeaver851

#### Pour se co au sql dans le conteneur de postgres

```bash
psql -U root -d blog
```

## Lister les ports des conteneurs

Liser les conteneurs

```bash
docker ps --format "table {{.Names}}\t{{.Ports}}"
```

par exemple

```bash
❯ docker ps --format "table {{.Names}}\t{{.Ports}}"
NAMES                    PORTS
nginx_learn_symfony      0.0.0.0:7851->80/tcp, [::]:7851->80/tcp
php_learn_symfony        9000/tcp
postgres_learn_symfony   5432/tcp
mailer_learn_symfony     1110/tcp, 0.0.0.0:32768->1025/tcp, [::]:32768->1025/tcp, 0.0.0.0:32769->8025/tcp, [::]:32769->8025/tcp
DBeaver_test-symfony     0.0.0.0:7852->8978/tcp, [::]:7852->8978/tcp
```

si je veux en arrêter uu.

```bash
docker stop DBeaver_test-symfony
docker rm DBeaver_test-symfony
```
