# Installer NodeJS

Le code ici permet d'installer la LTS dynamiquement (curl va chercher automatiquement la version) de NodeJS avec NPM (source depuis [nodejs.org](https://nodejs.org/fr/download)).

```bash
NVM_CMD=$(curl -s https://nodejs.org/fr/download | tr '\n' ' ' | grep -o 'curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v[0-9]\+\.[0-9]\+\.[0-9]\+/install.sh | bash')
LTS_VERSION=$(curl -s https://nodejs.org/dist/index.json | jq -r '.[] | select(.lts != false) | .version' | head -1 | cut -d. -f1 | tr -d 'v')
bash -c "$NVM_CMD"
\. "$HOME/.nvm/nvm.sh"
nvm install "$LTS_VERSION"
```

Pour vérifier votre installation

```bash
node -v
# Doit afficher "v24.13.1".
npm -v
# Doit afficher "11.8.0".
```

## Pour désinstaller

On le vire avec nvm

```bash
nvm deactivate
nvm uninstall 24
```

Et on le dégage du shell

```bash
sed -i '/NVM_DIR/d' ~/.zshrc
sed -i '/nvm.sh/d' ~/.zshrc
sed -i '/bash_completion/d' ~/.zshrc
source ~/.zshrc
```
