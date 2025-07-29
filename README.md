# symfony-docker-template
Modèle de projet Symfony 7.3 avec Docker, sans base de données.

✅ Étape 1 : Préparer le dossier de travail

```bash
mkdir <<monDuProjetSymfony>>
cd <<monDuProjetSymfony>>
```

✅ Étape 2 : Créer un `docker-compose.yml` **minimal**, sans `version`

```bash
services:
  php:
    image: php:8.3-cli
    container_name: <<nomDuContainer>>
    working_dir: /app
    command: tail -f /dev/null
    stdin_open: true
    tty: true
    ports:
      - "8000:8000"
```

✅ Étape 3 : Lancer le conteneur

```bash
docker compose up -d
```

✅ Étape 4 : entrer dans le contrainer 

```bash
docker compose exec php bash
```

✅ Étape 5 : Installer Composer dans le conteneur

```bash
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer
```

✅ Étape 6 : Installer la Symfony CLI dans le conteneur

```bash
curl -sS https://get.symfony.com/cli/installer | bash
mv /root/.symfony*/bin/symfony /usr/local/bin/symfony
```

✅ Étape 7 : Installer Git (exigé par Symfony CLI)

```bash
apt update && apt install -y git
```

✅ Étape 8 : Créer le projet Symfony 7.3 avec la CLI

```bash
symfony new <<nomDuProjetSymfony>> --version="7.3.x" --webapp
```

✅ Étape 9 : Copier le projet en local

```bash
docker cp <<nomDuContainer>>:/app/<<monDuProjetSymfony>> ./<<monDuProjetSymfony>>
```

✅ Étape 10 : Modifier le `docker-compose.yml` pour câbler le projet

```bash
cd my_project
php bin/console
```

✅ Étape 11 : Redémarrer le container 

```bash
docker compose down
docker compose up -d
```

✅ Étape 12 : faire un cache clear dans le container si besoin 

```bash
php bin/console cache:clear
```
