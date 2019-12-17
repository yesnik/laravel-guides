# API Resources

See [documentation](https://laravel.com/docs/master/eloquent-resources)

When building an API, you may need a transformation layer that sits between your 
Eloquent models and the JSON responses that are actually returned to your application's users.

API resources are made of 2 entities: 

- *resource class*. It represents a single model that needs to be transformed into a JSON structure.
- *resource collection*. It used for transforming collections of models into a JSON structure.

## Console commands

```bash
# Single resource
php artisan make:resource Product

# Collection resource
php artisan make:resource ProductCollection
```
Files will be created at `app/Http/Resources` folder.

## Example

File 

```php
class Product extends JsonResource
{
    public function toArray($request)
    {
        return [
            'id' => $this->id,
            'name' => $this->name,
            'detail' => $this->detail,
            'created_at' => $this->created_at->format('d/m/Y'),
            'updated_at' => $this->updated_at->format('d/m/Y'),
        ];
    }
}
```

Notice that we can access model properties directly from the `$this` variable. 
This is because a resource class will automatically 
proxy property and method access down to the underlying model for convenient access.
