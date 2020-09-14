# Docker Structure for PHP7 +\_Apache + MySQL

## Setup

- Define your database and app environment credentials

```sh
cp docker/credenciais/app/exemplo.env docker/credenciais/app/.env
cp docker/credenciais/database/exemplo.env docker/credenciais/database/.env
cp docker/apache2/conf-available/exemplo-security.conf docker/apache2/conf-available/security.conf
cp docker/apache2/sites-available/exemplo-site.conf docker/apache2/sites-available/site.conf
```

## How to run

```sh
docker-compose up
```
