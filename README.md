<h1 align="center">Laracamp</h1>

<div align="center">

![Laravel](https://img.shields.io/badge/-Laravel-05122A?style=flat&logo=laravel)&nbsp;
![Socialite](https://img.shields.io/badge/-Laravel%20Socialite-05122A?style=flat&logo=auth0)&nbsp;
![Midtrans](https://img.shields.io/badge/-Midtrans-05122A?style=flat&logo=visa)&nbsp;
![Mailtrap](https://img.shields.io/badge/-Mailtrap-05122A?style=flat&logo=mailtrap)&nbsp;

</div>

<img src="assets/preview.png" alt="Preview">

<p align="center">This repository is web application that aims to provide various features such as authentication, authorization, payment gateway, and email integration. This app is built using Laravel, Breeze (Authentication and Authorization), Socialite (OAuth Google), Midtrans (Payment Gateway), Mailtrap (Email)</p>

## Table of Contents

-   [Tech Stack](#tech-stack)
-   [Entity Relationship Diagram](#entity-relationship-diagram-erd)
-   [Running on Localhost](#running-on-localhost)
    -   [Clone this repository](#clone-this-repository)
    -   [Copy & fill .env](#copy--fill-env)
    -   [Application URL](#application-url)
    -   [Database Configuration](#database-configuration)
    -   [Email Configuration](#email-configuration)
    -   [OAuth Google Configuration](#oauth-google-configuration)
    -   [Midtrans Payment Gateway Configuration](#midtrans-payment-gateway-configuration)
    -   [Install dependency package](#install-dependency-package)
    -   [Generate key](#generate-key)
    -   [Running the migration and seeder](#running-the-migration-and-seeder)
    -   [Running the application](#running-the-application)
-   [Deployment](#deployment)
    -   [Virtual Private Server (VPS)](#virtual-private-server-vps)
        -   [Cloning the repository](#cloning-the-repository)
        -   [Update Repository & Upgrade Package](#update-repository--upgrade-package)
        -   [Install necessary package](#install-necessary-package)
        -   [Install composer](#install-composer)
        -   [Configure MariaDB](#configure-mariadb)
        -   [Configure Laravel](#configure-laravel)
        -   [Configure Nginx](#configure-nginx)
-   [Git Flow](#git-flow)
    -   [Initialize](#initialize)
    -   [Creating new feature](#creating-new-feature)
    -   [Finish the feature](#finish-the-feature)
    -   [Create a new release](#create-a-new-release)
    -   [Finish the release](#finish-the-release)
-   [License](#license)

## Tech Stack

-   [Laravel](https://laravel.com) (`Framework`): Laravel is a PHP framework designed for web development with an expressive and elegant syntax. It provides a comprehensive ecosystem with features such as routing, sessions, caching, and authentication, enabling developers to build robust and scalable web applications easily.
-   [Breeze](https://github.com/laravel/breeze) (`Authentication and Authorization`): Laravel Breeze is a simple and minimal starter kit for authentication. It offers basic implementations for login, registration, password reset, and email verification, allowing developers to quickly and easily integrate authentication into their applications.
-   [Socialite](https://github.com/laravel/socialite) (`OAuth Google`): Laravel Socialite provides a simple and expressive way to integrate OAuth authentication with various platforms, including Google. With Socialite, you can set up user login through their Google accounts with just a few lines of code.
-   [Midtrans](https://midtrans.com) (`Payment Gateway`): Midtrans is a payment gateway solution that allows the integration of online payment methods into your application. Supporting various payment methods like credit cards, bank transfers, and e-wallets, Midtrans helps you securely and easily accept payments.
-   [Mailtrap](https://mailtrap.io) (`Email`): Mailtrap is an email testing service designed to capture test emails sent from your application. With Mailtrap, you can verify and analyze emails without the risk of sending them to real users, making it invaluable in development and testing environments.

## Entity Relationship Diagram (ERD)

![Entity Relationship Diagram (ERD)](assets/erd.png)

## Running on Localhost

### Clone this repository

> **NOTE**: If you are using Laragon or XAMPP you can specify the clone directory destination to your `www` or `htdocs`, for example
>
> ```bash
> git clone https://github.com/armandwipangestu/laracamp-bwa.git Z:/laragon/www/laracamp-bwa && cd laracamp-bwa
> ```
>
> or
>
> ```bash
> git clone https://github.com/armandwipangestu/laracamp-bwa.git C:/xampp/htdocs/laracamp-bwa && cd laracamp-bwa
> ```
>
> But if you just running using php web server you can place the clone directory anywhere

```bash
git clone https://github.com/armandwipangestu/laracamp-bwa.git && cd laracamp-bwa
```

### Copy & Fill .env

```bash
cp .env.example .env
```

After `.env.example` copied to `.env` now fill with your own configuration at this variable

### Application URL

You can change this `APP_URL` variable with your own configuration, for example if I running with laragon, I use pretty url which is will create a Virtual Host and mapping the local domain to the web server like `https://laracamp-bwa.dev`.

If you running with the php web server you can just edit this variable with this value `http://localhost:8000`

```bash
APP_URL=http://localhost
```

### Database Configuration

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=root
DB_PASSWORD=
```

### Email Configuration

At this mail variable you can just signup and signin on [mailtrap.io](https://mailtrap.io) and then go to `inboxes` menu. At that page you will see the Integration Tab like this

![Mailtrap](assets/mailtrap.png)

After you have your own configuration just fill the `.env` variable on mail configuration using that credentials

> **NOTE**: Optional configuration
>
> ```bash
> MAIL_ENCRYPTION=tls
> MAIL_FROM_ADDRESS=noreply@laracamp.dev
> ```

```bash
MAIL_MAILER=smtp
MAIL_HOST=mailhog
MAIL_PORT=1025
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null
MAIL_FROM_ADDRESS=null
MAIL_FROM_NAME="${APP_NAME}"
```

### OAuth Google Configuration

For setup this OAuth variable you must be create a new Google Cloud Project on [console.cloud.google.com](https://console.cloud.google.com)

After creating a Google Cloud Project, you can go to the `API & Service` > `OAuth consent screen` page like this

![GCP OAuth consent screen](assets/gcp-oauth-consent-screen.png)

Still on that page, you can scroll down and fill list domain on `Authorized domains` section. This list domain will be use for the callback.

> **NOTE**: You can add list domain on this section, for example I use laragon pretty url so I can add `laravel-bwa.dev`. Or if you are using php web server you can add `localhost:8000`

![Authorized Domain](assets/gcp-oauth-consent-screen-authorized-domain.png)

Now you can finish the OAuth Google Configuration, you can `Save and Continue` until done.

After the configuration finished, now create the OAuth client credentials at `Credentials` page

![GCP Oauth Create Credentials](assets/gcp-oauth-create-credentials.png)

Choose `Application type` with `Web application` and fill the `Name` section. And then now fill the `Authorized redirect URIs`

> **NOTE**: You can add list domain on this section, for example I use laragon pretty url so I can add `laravel-bwa.dev`. Or if you are using php web server you can add `localhost:8000`. The domain will have endpoint with `/auth/google/callback`

![GCP Oauth Create OAuth Client ID](assets/gcp-oauth-create-oauth-client-id.png)

After all the configuration already fill click `Create`. Now you will see the alert with OAuth Credentials like this

![OAuth Secret](assets/oauth-secret.png)

Now you can fill this variable with that credentials

> **NOTE**: For the `GOOGLE_CLIENT_REDIRECT` you can use this configuration
>
> ```bash
> GOOGLE_CLIENT_REDIRECT=https://localhost:8000/auth/google/callback
> ```
>
> or
>
> ```bash
> GOOGLE_CLIENT_REDIRECT=https://laracamp-bwa.dev/auth/google/callback
> ```

```bash
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=
GOOGLE_CLIENT_REDIRECT=
```

### Midtrans Payment Gateway Configuration

To setup this variable you must be signup and sigin as merchant at [midtrans.com](https://midtrans.com)

After you signup and signin, go to dashboard and change the environment from `Production` to `Sandbox`

In environment `Sandbox` you can go to the `Settings` > `Access Keys` and you will see the configurations for credentials like this

![Midtrans Access Keys](assets/midtrans-access-keys.png)

Now you can fill this variable with that configuration

> **NOTE**: Optional configuration you can change the `Snap Preferences` at `Settings`, this configuration will affect to the view when user see the payment page
>
> ![Midtrans Snap Preferences](assets/midtrans-snap-preferences.png)

```bash
MIDTRANS_SERVER_KEY=
MIDTRANS_CLIENT_KEY=
MIDTRANS_IS_PRODUCTION=false
MIDTRANS_IS_SANITIZED=false
MIDTRANS_IS_3DS=false
```

Don't forget to add the `Notification URL` at `Settings` > `Payment`

![Midtrans Payment](assets/midtrans-payment.png)

> **NOTE**: You must use the online url (accessible on the internet), you can use `ngrok` or `vscode` port forwarding

![Midtrans Notification URL](assets/midtrans-notification-url.png)

### Install dependency package

```bash
composer install
```

### Generate key

```bash
php artisan key:generate
```

### Running the migration and seeder

```bash
php artisan migrate:fresh --seed
```

### Running the application

> **NOTE**: If you are using laragon pretty url like me, you can skip this part because it already running on local domain because virtual host. But this part will be use for the port forwarding (ngrok or vscode) and testing midtrans payment

```bash
php artisan serve
```

Now you can access the application on `http://localhost:8000`

## Deployment

### Virtual Private Server (VPS)

> **NOTE**: Do not forget to open the firewall to HTTP/s (80/443) port

In this VPS I'm using Ubuntu 24.04 LTS on Google Compute Engine

#### Cloning the repository

```bash
git clone https://github.com/armandwipangestu/laracamp-bwa.git ~/laracamp-bwa
```

#### Update Repository & Upgrade Package

```bash
sudo apt update && sudo apt upgrade
```

#### Install necessary package

```bash
sudo apt install php-mbstring php-xml php-bcmath php-curl php-cli php-fpm unzip mariadb-server
```

#### Install composer

```bash
curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php
HASH=`curl -sS https://composer.github.io/installer.sig` && echo $HASH
php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer
```

#### Configure MariaDB

1. Change default password for root user

```bash
sudo mariadb -u root -p
```

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'your_secure_password';
FLUSH PRIVILEGES;
```

2. MariaDB secure installation

```bash
mariadb-secure-installation
```

3. Create new database and user

```bash
sudo mariadb -u root -p
```

```sql
CREATE database laracamp_bwa;
CREATE USER user_laracamp_bwa IDENTIFIED BY 'your_secure_password';
GRANT ALL PRIVILEGES ON `laracamp_bwa`.`*` TO 'user_laracamp_bwa'@'localhost' IDENTIFIED BY 'your_secure_password';
FLUSH PRIVILEGES;
```

#### Configure Laravel

1. Install laravel dependency

> **NOTE**: You must be setup your `.env`, you can refer with the localhost setup

```bash
cd ~/laracamp-bwa && composer install
```

2. Generate key

```bash
php artisan key:generate
```

3. Running the migration and seeder

```bash
php artisan migrate:fresh --seed
```

4. Copy or move project to `/var/www/laracamp-bwa`

```bash
sudo cp ~/laracamp-bwa /var/www/laracamp-bwa
```

5. Change the user and group owner permission to `www-data`

```bash
sudo chown -R www-data:www-data /var/www/laracamp-bwa
```

6. Change the permission mode for `storage` and `bootstrap/cache` folder

```bash
sudo chmod -R 755 /var/www/laracamp-bwa/storage
sudo chmod -R 755 /var/www/laracamp-bwa/bootstrap/cache
```

#### Configure Nginx

1. Disable default nginx configuration

```bash
sudo rm /etc/nginx/sites-enabled/default
```

2. Copy nginx configuration

```bash
sudo cp ~/laracamp-bwa/nginx/laracamp.conf /etc/nginx/sites-available/laracamp.conf
```

3. Enable nginx configuration

```bash
sudo ln -s /etc/nginx/sites-avilable/laracamp.conf /etc/nginx/sites-enable/laracamp.conf
```

4. Restart Nginx service

```bash
sudo systemctl restart nginx
```

Now your application has been running.

## Git Flow

### Initialize

Start using git-flow by initializing it inside an existing git repository

> **NOTE**: Before running this command, create a new branch for developing the application
>
> ```bash
> git branch development
> ```

```bash
git flow init
```

Now choose the `main` branch as the production release and `development` branch as the development release

![Git Flow Init](assets/git-flow-init.png)

### Creating new feature

If you want to develop new feature for example `payment-gateway` you can create with git flow with this command

```bash
git flow feature start payment-gateway
```

![Git Flow Feature Start](assets/git-flow-feature-start.png)

After creating new feature you can start develop the feature

### Finish the feature

If your feature has been develop and finish, now you can merge the branch feature with the development branch with this command

```bash
git flow feature finish payment-gateway
```

![Git Flow Feature Finish](assets/git-flow-feature-finish.png)

### Create a new release

Everytime you finish the feature you can create a new release based on that code with this command

> **NOTE**: The `v1.1.0` is the release name

```bash
git flow release start v1.1.0
```

### Finish the release

The release has been created, now you can finish the release with this command

```bash
git flow release finish 'v1.1.0'
```

You can add release message for the feature you have been develop, for example `Release Payment Gateway Feature`

![Git Flow Release Finish](assets/git-flow-release-finish.png)

![Git Flow Release Finish 2](assets/git-flow-release-finish-2.png)

Now you can push the local branch repository to the remote repository (`development` and `main` branch)

But the push will not be create a tag and release on remote repository, to create that you must be push the version tag on local repository using this command

```bash
git push origin v1.1.0
```

![Git Flow Release Tag](assets/git-flow-release-tag.png)

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
