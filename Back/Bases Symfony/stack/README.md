# Docker et Symfony

on crée un projet ex nihilo, ça va créer un nouveau projet et initialiser le repo git

```bash
PROJECT_NAME="test_symfony"
symfony new $PROJECT_NAME --version="7.4.*" --webapp
cd $PROJECT_NAME
```

## Symfony sur Docker

Pour la concevoir cette pile de conteneurs, je me suis basé [sur ce tutoriel](https://www.youtube.com/watch?v=dBjOBV64bIg).
On paramètre les variables d’environnement.

```bash
mv compose.override.yaml compose.override.yaml.bak
mv compose.yaml compose.yaml.bak
USER_ID=$(id -u)
GROUP_ID=$(id -g)
cat <<EOF | cat - .env > temp && mv temp .env
DB_USER="root"
DB_PASSWORD="root"
DB_NAME="blog"
SERVER_VERSION="16"
DB_URL="postgresql://\${DB_USER}:\${DB_PASSWORD}@postgres:5432/\${DB_NAME}?serverVersion=\${SERVER_VERSION}&charset=utf8"
USER_ID="${USER_ID}"
GROUP_ID="${GROUP_ID}"
EOF
sed -i 's|postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8|${DB_URL}|' .env
```

On lance le daemon de Docker (ou sinon via Docker Desktop)

```bash
sudo systemctl start docker
```

Puis on lance la création de la pile.

```bash
docker compose -p $PROJECT_NAME up -d
```
