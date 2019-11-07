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

## Working with variables

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
