# Vehicle Owner Registry

`Cars_tables` is an academic web application for managing vehicle owner records. I built the core workflow in PHP and Laravel 10 using named web routes, controllers, Eloquent models and Blade views.

## Core workflow

- List owner records and filter the list by exact first name.
- Add, edit and delete an owner record with a first name, surname and phone number.
- Populate a local database with 50 synthetic owner records through the project seeder.

The owner registry is the main workflow. The repository also contains partial vehicle and model screens.

## Where to read the code

| File or folder | What it shows |
| --- | --- |
| [routes/web.php](routes/web.php) | Named routes linking the owner screens and forms to controller actions. |
| [OwnerController.php](app/Http/Controllers/OwnerController.php) | Loads records, applies the name filter and saves or deletes data through Eloquent. |
| [Owner.php](app/Models/Owner.php) | The Eloquent model for owner records. |
| [Owner views](resources/views/owners) | Blade templates for the list and forms. |
| [Migrations](database/migrations) and [seeders](database/seeders) | Database structure and synthetic examples for local use. |

For example, the owner filter sends a form request to `OwnerController::filter`. The controller queries the `Owner` model by first name and renders the same Blade list with the matching records.

## Local setup reference

Use PHP 8.3 with PDO SQLite, Composer 2 and Node.js 22 with npm. From the repository root, install the PHP dependencies and create a local SQLite file:

```sh
composer install
php -r "if (!file_exists('database/database.sqlite')) touch('database/database.sqlite');"
```

Create a local `.env` file at the repository root with these values:

```dotenv
APP_NAME=CarsTables
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://127.0.0.1:8000
DB_CONNECTION=sqlite
TELESCOPE_ENABLED=false
```

Generate the app key, prepare the database and build the frontend assets:

```sh
php artisan key:generate
php artisan migrate --seed
npm ci
npm run build
php artisan serve
```

Open `http://127.0.0.1:8000` for the owner list. These steps are a setup reference based on the checked-in files. The coursework app is intended for local evaluation with sample data.
