# Console commands

- `composer global require laravel/installer` - download the Laravel installer using Composer
- `php artisan db:seed` - seed database with `database/seeds/DatabaseSeeder.php`
- `laravel new mysite` - create project
- `php artisan route:list` - show routes
- `php artisan serve` - run development server
- `php artisan tinker` - run interactive console
- `php artisan migrate` - apply migrations

## Generate code

- `php artisan make:command DeleteOldProducts` - create `app/Console/Commands/DeleteOldProducts.php`
- `php artisan make:controller ArticlesController -r` - create controller (with CRUD actions)
- `php artisan make:factory EmployeeFactory --model=Employee` - create `database/factories/EmployeeFactory.php` for `Employee`
- `php artisan make:model Article -m` - create model with migration
- `php artisan notifications:table` - create migration for notifications table
- `php artisan make:notification ProductCreated` - create `app/Notifications/ProductCreated.php`
- `php artisan make:seeder EmployeesTableSeeder` - create `database/seeds/EmployeesTableSeeder.php`
