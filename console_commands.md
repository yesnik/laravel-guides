# Console commands

- `composer global require laravel/installer` - download the Laravel installer using Composer
- `laravel new mysite` - create project
- `php artisan config:clear` - clear configuration cache
- `php artisan route:list` - show routes
- `php artisan serve` - run development server
- `php artisan tinker` - run interactive console
- `php artisan migrate` - apply migrations
- `php artisan db:seed` - seed database with `database/seeds/DatabaseSeeder.php`

## Generate code

- `php artisan make:command DeleteOldProducts` - create `app/Console/Commands/DeleteOldProducts.php`
- `php artisan make:controller ArticlesController -r` - create controller (with CRUD actions)
- `php artisan make:controller API/ClaimController --api` - make controller for API (with CRUD actions)
- `php artisan make:factory EmployeeFactory --model=Employee` - create `database/factories/EmployeeFactory.php` for `Employee`
- `php artisan make:model Article -m` - create model with migration
- `php artisan make:notification ProductCreated` - create `app/Notifications/ProductCreated.php`
- `php artisan make:seeder EmployeesTableSeeder` - create `database/seeds/EmployeesTableSeeder.php`
- `php artisan make:test Http/Controllers/ClaimControllerTest` - create test file for feature

- `php artisan notifications:table` - create migration for notifications table
