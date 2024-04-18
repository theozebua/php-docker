# PHP Docker Environment

This is a repository that use Docker to develop PHP applications. If you want to develop a PHP application, this is the right repository that you can use.

This docker environment comes with:

- ✅ PHP (8.1, 8.2, 8.3)
- ✅ Composer (latest)
- ✅ Apache (latest)
- ✅ MySQL (latest)
- ✅ SQLite (3)
- ✅ phpMyAdmin (latest)

Soon:

- 🕔 Git
- 🕔 MariaDB
- 🕔 PostgreSQL
- 🕔 SQL Server
- 🕔 Redis

## Installation

- Clone this repository
- Delete the `.git` directory
- Copy `.env.example` to `.env`
- Select your `PHP_VERSION` in `.env`. Available versions: `8.1`, `8.2` and `8.3`.

## Running The Docker Environment

In this docker environment, we will use docker compose to run our services at once.

To run this docker environment, you simply type this:

```bash
sudo docker compose up -d

# or

sudo docker-compose up -d

# depends on your docker compose version
```

Then smash the `enter` button, and you are ready to go.

## Project Installation

- **[Laravel](https://laravel.com)**

```bash
sudo docker compose run --rm app rm .gitkeep && sudo docker compose run --rm app composer create-project laravel/laravel .
```

- **[Symfony](https://symfony.com)**

```bash
# run this if you are building a traditional web application
sudo docker compose run --rm app rm .gitkeep && sudo docker compose run --rm app composer create-project symfony/skeleton:"7.0.*" .

sudo docker compose run --rm app composer require webapp

# run this if you are building a microservice, console application or API
sudo docker compose run --rm app rm .gitkeep && sudo docker compose run --rm app composer create-project symfony/skeleton:"7.0.*" .
```

- **[Slim](https://slimframework.com/)**

```bash
sudo docker compose run --rm app rm .gitkeep && sudo docker compose run --rm app composer create-project slim/slim-skeleton .
```

If you want to install another framework, just run:

```bash
sudo docker compose run --rm app rm .gitkeep && sudo docker compose run --rm app composer create-project another/framework .
```

Or if you prefer not to use a framework, you can do that as well.

## Enter The Application Container

```bash
sudo docker exec -it app bash
```

> Note: If you run a development server with `php -S <host>:<port> -t public`, `php artisan serve` or any other console command that serve the application, make sure you set the host to `0.0.0.0` so it can be accessible from outside the container.

## Using Apache Web Server

If you want to use apache web server to serve your application, you can do that simply by creating a symlink from your application entrypoint to the web server entrypoint. By default, the web server entrypoint is in the `/var/www/html` directory.

**Example (Laravel)**

1. Enter the application container

```bash
sudo docker exec -it app bash
```

2. Remove the default web server entrypoint

```bash
sudo rm -rf /var/www/html
```

if it ask you for your password, just type `password` and hit `enter`.

3. Create a symlink from your application entrypoint to the web server entrypoint

```bash
sudo ln -s /home/me/application/public /var/www/html
```

4. Done ✅. Now, your application is served by the web server and you can access it on your local machine at `http://localhost:8080`.
