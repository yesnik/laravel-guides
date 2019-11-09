# Routes

## Call controller

```php
// routes/web.php

Route::get('/posts/{id}', 'PostsController@show')->name('posts.show');
```

## Call named route

In the view:

```blade
<a href="{{ route('posts.show', $post) }}">Some title</a>
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
