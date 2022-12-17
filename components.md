# Blade Components

See [docs](https://laravel.com/docs/master/blade#components)

## Class based components

Create component:

```bash
php artisan make:component Alert
```

This command will create:

- `app/View/Components/Alert.php`
- `resources/views/components/alert.blade.php`

At template:

```
<x-alert />
```

### Pass variable to component

View:

```
<x-alert message="Hello" />
```

Component:

```php
class Alert extends Component
{
    public string $message;

    public function __construct(string $message)
    {
        $this->message = $message;
    }

    public function render()
    {
        return view('components.alert');
    }
}
```
