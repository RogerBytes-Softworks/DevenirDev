# Installer NodeJS

Le code ici permet d'installer la LTS dynamiquement (curl va chercher automatiquement la version) de NodeJS avec NPM (source depuis [nodejs.org](https://nodejs.org/fr/download)).

```bash
NVM_CMD=$(curl -s https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh)
VERSION=$(curl -s https://nodejs.org/dist/index.json | jq -r '.[] | select(.lts != false) | .version' | head -1 | cut -d. -f1 | tr -d 'v')
bash -c "$NVM_CMD"
\. "$HOME/.nvm/nvm.sh"
nvm install "$VERSION"
```

Pour vérifier votre installation

```bash
node -v
# Doit afficher "v24.13.1".
npm -v
# Doit afficher "11.8.0".
```

## Pour installer la current

Si vous voulez la current au lieu de la LTS utilisez.

```bash
VERSION=$(curl -s https://nodejs.org/dist/index.json | jq -r '.[] | select(.lts == false) | .version' | head -1 | cut -d. -f1 | tr -d 'v')
```

## Pour désinstaller

On le vire avec nvm

```bash
nvm deactivate
nvm uninstall "$VERSION"
```

Et on le dégage du shell

```bash
sed -i '/NVM_DIR/d' ~/.zshrc
sed -i '/nvm.sh/d' ~/.zshrc
sed -i '/bash_completion/d' ~/.zshrc
source ~/.zshrc
```
