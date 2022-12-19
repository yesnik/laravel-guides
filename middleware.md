# Middleware

### Generate file

```bash
php artisan make:middleware QueryCheck
```

File `/app/Http/Middleware/QueryCheck.php` will be created:

```php
class QueryCheck
{
    public function handle(Request $request, Closure $next)
    {
        if (!$request->has('q')) {
            abort(403);
        }
        return $next($request);
    }
}
```

### Register new middleware

Edit `app/Http/Kernel.php`. We can add it to global middleware:

```php
protected $middleware = [
    // ...
    QueryCheck::class,
];
```

Or we can add it to route middleware:

```php
    protected $routeMiddleware = [
        // ...
        'q' => QueryCheck::class,
    ];
```

### Apply middleware to route

Edit `routes/web.php`:

```php
Route::get('/', function () {
    return view('welcome');
})->middleware('q');
```
