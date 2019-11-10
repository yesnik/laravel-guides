# Factories

## Console commands

**Generate factory class**

```bash
php artisan make:factory ArticleFactory -m 'App\Article'
```

**Generate records using factory**

```php
php artisan tinker

>>> factory(App\User::class, 5)->create()
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

