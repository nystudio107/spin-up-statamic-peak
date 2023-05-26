# Spin Up Craft 4.4 Beta

If you want to give the popular Statamic [Peak starter kit](https://statamic.com/starter-kits/studio1902/peak) a try without having to do any setup, this project is for you!

It allows you to spin up the Statamic [Peak starter kit](https://statamic.com/starter-kits/studio1902/peak) in your browser via Github Codespaces, or on your local computer with a few quick commands.

Whether in-browser or on your local computer, you'll have a fully functional Statamic [Peak starter kit](https://statamic.com/starter-kits/studio1902/peak) instance with an editor, content, Twig templates, and a database.

This project was created using [Spin Up Statamic](https://github.com/nystudio107/spin-up-statamic)

## Spin Up Statamic Peak in a browser via Github Codespaces

1. Click this button:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?hide_repo_select=true&ref=master&repo=605680287)

3. In the resulting Terminal window, type `make dev` to start the project up
3. Wait until you see output like this, and then access the site via the credentials that are output on the console:

```
php_1    | ### Your Statamic site is ready!
php_1    | Frontend URL: https://khalwat-laughing-space-zebra-xg9qxvqjpqhp5qx-8050.preview.app.github.dev/
php_1    | CP URL: https://khalwat-laughing-space-zebra-xg9qxvqjpqhp5qx-8050.preview.app.github.dev/cp
php_1    | CP User: demo@statamic.com
php_1    | CP Password: password
```

This lets anyone use the project without having to do _any_ local setup.

You can use the Codespaces editor to edit Twig files, load the site frontend, or log into the Craft CP, all from within a browser!

The first time you start up your project in Codespaces, it'll take some time to set everything up. However, subsequent startups will be very quick.

You can access your existing Codespaces here:

https://github.com/codespaces

Click on one to resume it. If you don't see a Terminal window, go to the hamburger  menu in the top-left, and click on **Terminal > New Terminal**

You are limited to 15 active Codespaces on the free plan, but you can go in and delete any older Codespaces you're not using at any time.

## Spin Up Statamic Peak in local dev

1. Have [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed
2. Clone this repository down with `git clone https://github.com/nystudio107/spin-up-statamic-peak.git`
3. `cd` to your repo in your terminal
4. Get the project up and running with `make dev`
5. Wait until you see output like this, and then access the site via the credentials that are output on the console:

```
spin-up-craft-44-beta-php-1    | ### Your Statamic site is ready!
spin-up-craft-44-beta-php-1    | Frontend URL: http://localhost:8050/
spin-up-craft-44-beta-php-1    | CP URL: http://localhost:8050/cp
spin-up-craft-44-beta-php-1    | CP User: demo@statamic.com
spin-up-craft-44-beta-php-1    | CP Password: password
```

Hit `Control-C` to terminate the project and spin down the containers

The first time you start up your project, it'll take some time to set everything up. However, subsequent startups will be very quick.

## Available `make` commands

This project uses `make` to execute various commands in the appropriate containers. Here's a list of available commands:

This project uses `make` to execute various commands in the appropriate containers. Here's a list of available commands:

* `make dev` - Start the dev server
* `make artisan xxx` - Execute a `php artisan` CLI command in the PHP container
* `make composer xxx` - Execute a `composer` command in the PHP container
* `make npm xxx` - Execute an `npm` command in the PHP container
* `make please xxx` - Execute a `please` command in the PHP container
* `make statamic xxx` - Execute a `statamic` CLI command in the PHP container
* `make ssh` - Open up a shell in the PHP container

If the project is already running via `make dev` you can use a second terminal tab/window to execute additional commands.

## Random notes

- The `.env` file is created by copying `example.env` file when you start the project up
- The server will use the `INITIAL_SERVER_PORT` in the `.env` file for the initial port to start looking for unused ports from. It will increment it until it finds and unused port, and then use it
- If instead you want to used a fixed port, you can explicitly set the `DEV_SERVER_PORT` in the `.env` file
- The Docker containers will be named after the project directory, so give it a unique name for each project

## To Do

- Enjoy kicking Statamic Peak's tires!

Brought to you by [nystudio107](https://nystudio107.com/)

The rest of the Peak starter kit README.md follows:

.....

# site.ext

## Installation instructions

1. run `composer install`
2. run `php please make:user`
3. run `npm i` && `npm run dev`

## Environment file contents

### Development

```env
Dump your .env values here with sensitive data removed.
```

### Production

```env
Dump your .env values here with sensitive data removed. The following is a production example that uses full static caching:
APP_NAME="Peak"
APP_ENV=production
APP_KEY="base64:AuTWNJZiYkZV5JBW8S+e9U2LE9HsZte2iuGgX/BOy4E="
APP_DEBUG=false
APP_URL=

DEBUGBAR_ENABLED=false

LOG_CHANNEL=stack

BROADCAST_DRIVER=log
CACHE_DRIVER=file
QUEUE_CONNECTION=redis
SESSION_DRIVER=file
SESSION_LIFETIME=120

REDIS_HOST=127.0.0.1
REDIS_DATABASE=
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_MAILER=smtp
MAIL_HOST=smtp.postmarkapp.com
MAIL_PORT=587
MAIL_ENCRYPTION=tls
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM_ADDRESS=
MAIL_FROM_NAME="${APP_NAME}"

IMAGE_MANIPULATION_DRIVER=imagick

STATAMIC_LICENSE_KEY=
STATAMIC_THEME=business

STATAMIC_API_ENABLED=false
STATAMIC_REVISIONS_ENABLED=false

STATAMIC_GIT_ENABLED=true
STATAMIC_GIT_PUSH=true
STATAMIC_GIT_DISPATCH_DELAY=5

STATAMIC_STATIC_CACHING_STRATEGY=full
SAVE_CACHED_IMAGES=false
STATAMIC_STACHE_WATCHER=false
STATAMIC_CACHE_TAGS_ENABLED=true

#STATAMIC_CUSTOM_CMS_NAME=
STATAMIC_CUSTOM_LOGO_OUTSIDE_URL="/visuals/client-logo.svg"
#STATAMIC_CUSTOM_LOGO_NAV_URL=
#STATAMIC_CUSTOM_FAVICON_URL=
#STATAMIC_CUSTOM_CSS_URL=
```

## NGINX config

Add the following to your NGINX config __inside the server block__ enable static resource caching:
```
expires $expires;
```

And this __outside the server block__:
```
map $sent_http_content_type $expires {
    default    off;
    text/css    max;
    ~image/    max;
    application/javascript    max;
    application/octet-stream    max;
}
```

## Deploy script Ploi

```bash
if [[ {COMMIT_MESSAGE} =~ "[BOT]" ]]; then
    echo "Automatically committed on production. Nothing to deploy."
    {DO_NOT_NOTIFY}
    # Uncomment the following line when using zero downtime deployments.
    # {CLEAR_NEW_RELEASE}
    exit 0
fi

cd {SITE_DIRECTORY}
git pull origin {BRANCH}
composer install --no-interaction --prefer-dist --optimize-autoloader --no-dev

npm ci
npm run build
{SITE_PHP} artisan cache:clear
{SITE_PHP} artisan config:cache
{SITE_PHP} artisan route:cache
{SITE_PHP} artisan statamic:stache:warm
{SITE_PHP} artisan queue:restart
{SITE_PHP} artisan statamic:search:update --all
{SITE_PHP} artisan statamic:static:clear
{SITE_PHP} artisan statamic:static:warm --queue

{RELOAD_PHP_FPM}

echo "🚀 Application deployed!"
```

## Deploy script Forge

```bash
if [[ $FORGE_DEPLOY_MESSAGE =~ "[BOT]" ]]; then
    echo "Automatically committed on production. Nothing to deploy."
    exit 0
fi

cd $FORGE_SITE_PATH
git pull origin $FORGE_SITE_BRANCH
$FORGE_COMPOSER install --no-interaction --prefer-dist --optimize-autoloader --no-dev

npm ci
npm run build
$FORGE_PHP artisan cache:clear
$FORGE_PHP artisan config:cache
$FORGE_PHP artisan route:cache
$FORGE_PHP artisan statamic:stache:warm
$FORGE_PHP artisan queue:restart
$FORGE_PHP artisan statamic:search:update --all
$FORGE_PHP artisan statamic:static:clear
$FORGE_PHP artisan statamic:static:warm --queue

( flock -w 10 9 || exit 1
    echo 'Restarting FPM...'; sudo -S service $FORGE_PHP_FPM reload ) 9>/tmp/fpmlock
```
