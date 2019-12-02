# Factories

PHP library [Faker](https://github.com/fzaninotto/Faker) is used to generate fake values.

## Console commands

**Generate factory class**

```bash
php artisan make:factory ArticleFactory -m 'App\Article'
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

```php
$factory->define(Article::class, function (Faker $faker) {
    return [
        'title' => $faker->sentence,
        'excerpt' => $faker->sentence,
        'body' => $faker->paragraph,
        'user_id' => factory(\App\User::class),
    ];
});
```
