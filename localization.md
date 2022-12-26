# Localization

See [docs](https://laravel.com/docs/master/localization)

## Define translations

Define translations for English at `lang/en/profile.php`:
```php
return [
    'welcome' => 'Welcome',
];
```

Define translations for Russian at `lang/ru/profile.php`:
```php
return [
    'welcome' => 'Добро пожаловать',
];
    ```

## Activate default locale

Edit `config/app.php`:

```php
return [
    // ...
    'locale' => 'ru',
];
```
## Use translaton in the view

Edit file `resources/views/profile.blade.php`:

```blade
<h1>{{ __('profile.welcome') }}</h1>
```

## Set locale via Route

Edit `/routes/web.php`:

```php
Route::get('/{locale}/profile', function ($locale) {
    if (! in_array($locale, ['en', 'ru'])) {
        abort(400);
    }

    \Illuminate\Support\Facades\App::setLocale($locale);

    return view('profile');
});
```
