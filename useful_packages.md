# Useful Laravel Packages



## jwt-auth

[jwt-auth](https://github.com/tymondesigns/jwt-auth) is JSON Web Token Authentication for Laravel & Lumen.

*Note*: instead of this package we can use [Laravel Passport](https://laravel.com/docs/master/passport).

## laravel/passport

[laravel/passport](https://laravel.com/docs/master/passport) makes API authentication a breeze. It provides a full OAuth2 server implementation for your Laravel application. It allows us to secure our routes.
Just use `api:auth` middleware:

```php
// routes/api.php
Route::resource('claims', 'API\ClaimController')
    ->middleware('auth:api');
```

## laravel/ui

[laravel/ui](https://github.com/laravel/ui) provides the Bootstrap, Vue, React scaffolding for Laravel app.

Integrate *bootstrap*, *jquery* in the project, create views for authentication in the `resources/views/auth`:

```bash
php artisan ui bootstrap --auth

# Run this if you want to add React support
php artisan ui react --auth
```
