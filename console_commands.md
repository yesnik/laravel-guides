# Console commands

- `composer global require laravel/installer` - download the Laravel installer using Composer
- `php artisan db:seed` - seed database with `database/seeds/DatabaseSeeder.php`
- `laravel new mysite` - create project
- `php artisan serve` - run development server
- `php artisan tinker` - run interactive console
- `php artisan migrate` - apply migrations

## Generate code

- `php artisan make:controller ArticlesController` - create controller
- `php artisan make:factory EmployeeFactory --model=Employee` - create `database/factories/EmployeeFactory.php` for `Employee`
- `php artisan make:model Article -m` - create model with migration
- `php artisan make:seeder EmployeesTableSeeder` - create `database/seeds/EmployeesTableSeeder.php`
