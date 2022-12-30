# Factories

See [docs](https://laravel.com/docs/master/eloquent-factories)

PHP library [Faker](https://github.com/FakerPHP/Faker) is used to generate fake values.

### Generate factory class

```bash
php artisan make:factory Post
```

This command will create `database/factories/PostFactory.php`:

```php
namespace Database\Factories;

use App\Models\User;
use Illuminate\Database\Eloquent\Factories\Factory;

class PostFactory extends Factory
{
    public function definition()
    {
        return [
            'user_id' => User::factory(),
            'title' => $this->faker->sentence(),
            'body' => $this->faker->paragraph(),
        ];
    }
}
```

Run tinker and create 10 records for Post:

```
php artisan tinker

>>> App\Models\Post::factory(10)->create()
```

### Generate seeder

```bash
php artisan make:seeder EmployeeSeeder
```

This command will create file `database/seeds/EmployeeSeeder.php`:

```php
use Illuminate\Database\Seeder;

class EmployeeSeeder extends Seeder
{
    public function run()
    {
        App\Models\Employee::factory(10)->create();
    }
}
```

In `run()` we can create related models. Employee has many tasks:

```php
App\Models\Employee::factory(10)
    ->hasTasks(25)->create();
```

### Seed database

```bash
php artisan db:seed
```

### Generate records using factory

```bash
php artisan tinker
```

Laravel >= 8:
```php
User::factory()->count(50)->create();
```

Laravel < 8:
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

### Call custom seeder from DatabaseSeeder

Edit file `database/seeds/DatabaseSeeder.php`:

```php
class DatabaseSeeder extends Seeder
{
    public function run()
    {
        $this->call(EmployeeSeeder::class);
    }
}
```
