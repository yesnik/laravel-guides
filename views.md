# Views

## Extend layout

File: `resources/views/welcome.blade.php`:

```blade
@extends('layout')

@section('content')
    <p>Hello world!</p>
@endsection
```

File `resources/views/layout.blade.php`:

```blade
<!DOCTYPE html>
<head>
    <meta charset="utf-8">
</head>
<body>
    @yield('content')
</body>
</html>
```

## Show Pagination links

```blade
{!! $products->links() !!}
```

## Helper methods

### old()

Display the previous value of variable in case of error:

```blade
<input type="text" name="last_name" value={{ old('last_name') }}>
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

### @foreach

```php
@foreach ($products as $product)
  <tr>
    <td>{{ $product->id }}</td>
    <td>{{ $product->name }}</td>
  </tr>
@endforeach
```
