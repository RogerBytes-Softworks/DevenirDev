# Déploiement Docker

Dans cette documentation, nous allons créer un projet Symfony et le déployer dans une pile de conteneurs Docker.
Ceci est basé [la doc de Symfony sur Docker](https://symfony.com/doc/current/setup/docker.html), [la doc d'install de Symfony](https://symfony.com/download) ainsi que [cette vidéo de Devscast](https://www.youtube.com/watch?v=dBjOBV64bIg).

## Initialisation d'un nouveau projet Symfony

### Création de projet via CLI

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

Il retourne `7.4.3` pour la LTS : l'on pourra donc passer l'argument `--version="7.4.*"` ou `--version=lts` juste après.

On définit un nom de projet

```bash
PROJECT_NAME="LearnSymfony"
```

On se met dans le répertoire où l'on souhaite créer le projet, puis

```bash
symfony new $PROJECT_NAME --webapp --version=lts
cd $PROJECT_NAME
```

Cela a créé le projet complet (et déplacé à l'intérieur), pour faire une version "skeleton", il vous suffit de retirer l'argument `--webapp` de la commande.

On vérifie qu'il fonctionne en local

```bash
symfony serve
```

Et on se connecte à `http://127.0.0.1:8000/`, si le site apparaît, tout est bon.

  </div>
</details>

### Sécurisation des fichiers et repo

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On sécurise les .env sensibles (.env.local et dérivés sont déjà dans le `.gitignore`)

```bash
echo ".env.dev" >> .gitignore
echo ".env.test" >> .gitignore
git rm --cached .env.dev .env.test
git add .
git commit -m "Initial commit"
```

Il nous reste à créer notre repo sur github.

```bash
gh repo create "$PROJECT_NAME" --public
```

et à y lier notre branche locale :

```bash
ACCOUNT="RogerBytes"
git remote add origin git@github.com:"$ACCOUNT/$PROJECT_NAME".git
```

Puis notre commit

```bash
touch README.md
git add --all && git commit -m "First commit"
```

Suivi du premier push

```bash
git push -u origin master
```

  </div>
</details>

## Docker

<details>
  <summary class="button">
    Spoiler
  </summary>
  <div class="spoiler">

On commence par archiver les fichiers docker générés automatiquement (pour pouvoir utiliser notre compose personnalisé).

```bash
mv compose.override.yaml compose.override.yaml.bak
mv compose.yaml compose.yaml.bak
```

Ici l'on créé le `env.local` et l'on lui met les variables tels qu'identifiants et mots de passe de DB.

```bash
USER_ID=$(id -u)
GROUP_ID=$(id -g)
cat <<EOF > .env.local
DB_USER="root"
DB_PASSWORD="root"
DB_NAME="blog"
SERVER_VERSION="16"
USER_ID="${USER_ID}"
GROUP_ID="${GROUP_ID}"
DATABASE_URL="postgresql://\${DB_USER}:\${DB_PASSWORD}@postgres:5432/\${DB_NAME}?serverVersion=\${SERVER_VERSION}&charset=utf8"
EOF
```

On télécharge le compose personnalisé

```bash
mkdir temp_repo
git clone --filter=blob:none --no-checkout https://github.com/RogerBytes-Softworks/DevenirDev.git temp_repo
cd temp_repo
git sparse-checkout init --cone
git sparse-checkout set "Back/Bases Symfony/stack"
git checkout HEAD
cp -r "Back/Bases Symfony/stack/." ../
cd ..
rm -rf temp_repo
```

On ouvre `compose.yml` et on modifie les `container_name`, les noms de conteneurs doivent être unique, pareil pour le port forwarding, les port sortant (les premiers) doivent êtres uniques.

J'utilise cette convention de nommage

```yml
container_name: NOM_SERVICE_NOM_PROJET
```

qui donne

```yml
container_name: mailer_LearnSymfony
```

On lance le daemon de Docker (ou sinon via Docker Desktop)

```bash
sudo systemctl start docker
```

Puis on lance la création de la pile.

```bash
docker compose -p $PROJECT_NAME up -d
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
.button:hover {
  background-color: #217dbb;
}
details[open] .button {
  background-color: #1abc9c;
}
</style>
