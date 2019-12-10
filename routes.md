# Routes

## Call controller

```php
// routes/web.php

Route::get('/posts/{id}', 'PostsController@show')->name('posts.show');
Route::get('/articles', 'ArticlesController@index')->name('articles.index');
```

## Call named route

In the view:

```blade
<a href="{{ route('posts.show', $post) }}">Some title</a>
```

If you want to add GET-param `?tag=python` to the link:

```blade
<a href="{{ route('articles.index', ['tag' => 'python']) }}">Python articles</a>
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

