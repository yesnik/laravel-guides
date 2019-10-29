# Models

## Generate model

```bash
php artisan make:model Post

# with migration and controller
php artisan make:model Post -mc
```

## Eloquent ORM methods

```php
App\Post::all();

App\Post::first();

App\Post::where('published', true)->get();
```
