# Routes

## List routes

```bash
php artisan route:list
```

## Call controller

```php
// routes/web.php
Route::get('/posts/{id}', 'PostsController@show')->name('posts.show');
Route::get('/articles', 'ArticlesController@index')->name('articles.index');
```

## Group routes

```php
// routes/web.php
Route::controller(PostsController::class)->group(function() {
    Route::get('/posts', 'index');
    Route::get('/posts/{post}', 'show');
    Route::post('/posts', 'store');
});
```

### Prefix routes

```php
Route::prefix('/news')->group(function() {
    Route::get('/', [\App\Http\Controllers\IndexController::class, 'index']);
});
```

## Routes for API

```php
// routes/api.php

// URL: /api/test
Route::get('/test', function (Request $request) {
    return ['greeting' => 'Hello user!'];
});
```

## Route for resource

```php
Route::resource('/articles', ArticleController::class);
```
It will provide 7 CRUD actions for `ArticleController`:


| Method    | URI                     | Name             | Action                                         | Middleware   |
|-----------|-------------------------|------------------|------------------------------------------------|--------------|
| GET|HEAD  | articles                | articles.index   | App\Http\Controllers\ArticleController@index   | web          |
| POST      | articles                | articles.store   | App\Http\Controllers\ArticleController@store   | web          |
| GET|HEAD  | articles/create         | articles.create  | App\Http\Controllers\ArticleController@create  | web          |
| GET|HEAD  | articles/{article}      | articles.show    | App\Http\Controllers\ArticleController@show    | web          |
| PUT|PATCH | articles/{article}      | articles.update  | App\Http\Controllers\ArticleController@update  | web          |
| DELETE    | articles/{article}      | articles.destroy | App\Http\Controllers\ArticleController@destroy | web          |
| GET|HEAD  | articles/{article}/edit | articles.edit    | App\Http\Controllers\ArticleController@edit    | web          |

## Call named route

In the view:

```blade
<a href="{{ route('posts.show', $post) }}">Some title</a>
```

If you want to add GET-param `?tag=python` to the link:

```blade
<a href="{{ route('articles.index', ['tag' => 'python']) }}">Python articles</a>
```

## Route to view

Visiting `/about` URI will open `about.blade.php` view:

```php
Route::view('/about', 'about');
```

## Pass variable to view

```php
// routes/web.php

Route::get('/hello', function() {
    return view('hello', [
        'name' => request('name'),
    ]);
});
```

In the template `resources/view/hello.blade.php`:

```
<h1>Hello {{ $name }}</h1>
```

PHP doesn't undestand blade syntax, so Laravel converts 
this template to PHP-file and puts it to `storage/framework/views/***.php`

## Add wildcard to route

```php
// routes/web.php

Route::get('/posts/{id}', function($id) {
    return $id;
});
```
If we access URI */posts/123* then `$id` will be *123*.

## Show 404 page

```php
// routes/web.php

Route::get('/posts/{id}', function($id) {
    // ...
    abort(404, 'Post not found');
});
```

## Disable CSRF protection for URL

Add URL to `$except` variable at `app/Http/Middleware/VerifyCsrfToken.php`:

```php
/**
 * The URIs that should be excluded from CSRF verification.
 *
 * @var array
 */
protected $except = [
    '/home/postShow',
];
```

## Redirect to named route

```php
Route::get('/', function () {
    return view('welcome');
})->name('home');

Route::get('red', function () {
    // return redirect()->route('home');
    return to_route('home');
});
```

## Scope bindings

```php
Route::get('/users/{user}/posts/{post}', function (\App\Models\User $user, \App\Models\Post $post) {
    return $post;
})->scopeBindings();
```
This route will show post 5 created by user 1: /users/1/posts/5
