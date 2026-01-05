# Utilisation de Symfony

Ici on apprend à utiliser Symfony, et plus précisément une stack Docker.

## Se connecter au conteneur

<details><summary class="button">Spoiler</summary><div class="spoiler">

Symfony est installé dans php, ici, c'est dans le conteneur container_name: php_learn_symfony donc `caca`

```bash
docker exec -it php_learn_symfony bash
composer install
git config --global --add safe.directory /var/www
exit
docker compose restart php_learn_symfony
```

</div></details>

<style>.spoiler{border-left:4px solid #1abc9c;border-bottom-left-radius:3px;padding-left:10px;padding-top:15px;margin-top:-10px;margin-bottom:15px}.button{cursor:pointer;padding:5px 10px;background-color:#3498db;color:white;border-radius:3px;margin-bottom:5px;display:inline-block;transition:background-color 0.2s}.button:hover{background-color:#217dbb}details[open] .button{background-color:#1abc9c}</style>
