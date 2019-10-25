# Views

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
