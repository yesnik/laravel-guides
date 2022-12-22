# HTTP Session

See [docs](https://laravel.com/docs/master/session)

Laravel ships with a variety of session backends that are accessed through an expressive, unified API. 
Support for popular backends such as Memcached, Redis, and databases is included.

Config file: `/config/session.php`

## In Controller

### Save key and value to session

```php
public function login(Request $request)
{
    // ...
    $request->session()->put('login', 'some value');
}
```

### Remove key from session

```php
public function logout(Request $request)
{
    $request->session()->remove('login');

    return redirect('/');
}
```

## In the view

### Get value from session by key

```php
session()->get('login', 'Stranger') 
```

## Flash messages

### In the controller

```php
$request->session()->flash('success', 'Login was successful!');
```

### In the view

```php
@if(session('success'))
    <p style="color: green">
        {{ session('success') }}
    </p>
@endif
```
