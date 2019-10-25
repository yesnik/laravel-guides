# Views

## Working with variables

**Escape variable**

```blade
{{ $name }}
```

Laravel applies `htmlspecialchars()` to this variable.

**Don't escape variable**

```blade
{!! $name !!}
```
