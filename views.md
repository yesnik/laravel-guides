# Views

## Config

Config is located at `config/view.php`.

### Change views folder

At `config/view.php` we can define folder `resources/templates` for our views:

```php
    'paths' => [
        // resource_path('views'),
        resource_path('templates'),
    ],
```


## Components

File `resources/views/home.blade.php`:

```blade
<x-layout>
    <h1>Hello from Home</h1>
</x-layout>
```

Define `x-layout` component at `resources/views/Components/layout.blade.php`:

```blade
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <nav>
        <x-nav-link href="/">Home</x-nav-link>
        <x-nav-link href="/about">About</x-nav-link>
        <x-nav-link href="/contact">Contact</x-nav-link>
    </nav>
    {{ $slot }}
</body>
</html>
```

Component can accept attributes. Define `x-nav-link` component at `resources/views/Components/nav-link.blade.php`:

```blade
<a {{ $attributes }}>{{ $slot }}</a>
```

## Extend layout

File: `resources/views/welcome.blade.php`:

```blade
@extends('layout')

@section('title', 'Welcome to our site')

@section('content')
    <p>Hello world!</p>
@endsection
```

File `resources/views/layout.blade.php`:

```blade
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
    <title>@yield('title')</title>
</head>
<body>
    @yield('content')
</body>
</html>
```

## Output html / Disable escaping

This string will not be escaped with `htmlspecialchars`:

```blade
{!! '<a href="/">link</a>' !!}
```

## Helper methods

### old()

Display the previous value of variable in case of error:

```blade
<input type="text" name="last_name" value={{ old('last_name') }}>
```

### method_field()

Send form via PUT, DELETE, etc. http-method:

```blade
<form action="/users/login" method="post">
    {{ method_field('put') }}
</form>
```

## Working with variables

### Escaping

Views are located at `resources/views` folder.

**Escape variable**

```blade
{{ $name }}
```

Laravel applies `htmlspecialchars()` to this variable.

**Don't escape variable**

```blade
{!! $name !!}
```

## Add script

```blade
<script src="{{ asset('js/app.js')}}"></script>
```

Or with vitejs:

```blade
@vite('resources/js/app.js')
```
This will create 2 tags:

```html
<script type="module" src="http://127.0.0.1:5173/@vite/client"></script>
<script type="module" src="http://127.0.0.1:5173/resources/js/app.js"></script>
```

## Add CSS styles

```blade
<link href="{{ asset('css/app.css') }}" rel="stylesheet">
```

## Directives

### @error

Within an `@error` directive, you may echo the `$message` variable to display the error message.

```blade
<!-- /resources/views/post/create.blade.php -->

<input id="title" type="text" class="@error('title') is-invalid @enderror">

@error('title')
    <div class="alert alert-danger">{{ $message }}</div>
@enderror
```

### @if

```php
@if (Session::has('success'))
  <div class="alert alert-success">

  {{ Session::get('success') }}

  @php
    Session::forget('success');
  @endphp

  </div>
@endif
```

### @include

The included view *will inherit all data* available in the parent view.
Also we can pass an array of extra data to the included view.

```php
@include('product.form', ['name' => 'Kenny'])
```

### @foreach

```php
@foreach ($products as $product)
  <tr>
    <td>{{ $product->id }}</td>
    <td>{{ $product->name }}</td>
  </tr>
@endforeach
```

### URL

Get current page URL:

```blade
{{ Url::current() }}
```

Previous page URL:

```blade
{{ Url::previous() }}
```

Absolute URL for URI - `http://127.0.0.1:8000/about`:

```blade
{{ Url::to('/about') }}
```

## Cache

Compiled view's version will be stored in the PHP-file, e.g. `storage/framework/views/25a721855d6d38279393dbd0d93c7e0aff44226a.php`.

Clear compiled views:

```bash
php artisan view:clear
```
