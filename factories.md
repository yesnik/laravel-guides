# Factories

PHP library [Faker](https://github.com/fzaninotto/Faker) is used to generate fake values.

## Console commands

**Generate factory class**

```bash
php artisan make:factory EmployeeFactory --model=Employee
```

This command will create `database/factories/EmployeeFactory.php`. Edit this file:

```php
use App\Employee;
use Faker\Generator as Faker;

$factory->define(Employee::class, function (Faker $faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->unique->companyEmail,
        'start_date' => $faker->date,
        'due_date' => $faker->date 
    ];
});
```

**Generate seeder**

```bash
php artisan make:seeder EmployeesTableSeeder
```

This command will create file `database/seeds/EmployeesTableSeeder.php`. Edit this file:

```php
use Illuminate\Database\Seeder;

class EmployeesTableSeeder extends Seeder
{
    public function run()
    {
        factory(App\Employee::class, 50)->create();
    }
}
```

**Call custom seeder from DatabaseSeeder**

Edit file `database/seeds/DatabaseSeeder.php`:

```php
class DatabaseSeeder extends Seeder
{
    public function run()
    {
        $this->call(EmployeesTableSeeder::class);
    }
}
```

**Seed database**

```bash
php artisan db:seed
```

**Generate records using factory**

```bash
php artisan tinker
```
```php
// Create 5 records of User
factory(App\User::class, 5)->create()

// Create 3 articles for user with id = 5
factory(App\Article::class, 3)->create(['user_id' => 5])
```

## Factory example 

File `database/factories/UserFactory.php`:

```php
$factory->define(User::class, function (Faker $faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->unique()->safeEmail,
        'email_verified_at' => now(),
        'password' => '$2y$10$92IXUNpkjO0rOQ5byMi.Ye4oKoEa3Ro9llC/.og/at2.uheWG/igi', // password
        'remember_token' => Str::random(10),
    ];
});
```

We can create related entity - `App\User`:

```php
$factory->define(Article::class, function (Faker $faker) {
    return [
        'title' => $faker->title,
        'excerpt' => $faker->sentence,
        'body' => $faker->paragraph,
        'user_id' => factory(\App\User::class),
    ];
});
```

```php
$factory->define(Employee::class, function (Faker $faker) {
    return [
        'name' => $faker->name,
        'email' => $faker->unique->companyEmail,
        'start_date' => $faker->date,
        'due_date' => $faker->date 
    ];
});
```
