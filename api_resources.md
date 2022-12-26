# API Resources

See [documentation](https://laravel.com/docs/master/eloquent-resources)

When building an API, you may need a transformation layer that sits between your 
Eloquent models and the JSON responses that are actually returned to your application's users.

API resources are made of 2 entities: 

- *resource class*. It represents a single model that needs to be transformed into a JSON structure.
- *resource collection*. It used for transforming collections of models into a JSON structure.

## Console commands

```bash
# Create a resource class
php artisan make:resource ProductResource

# Create a resource collection
php artisan make:resource ProductCollection
```
Files will be created at `app/Http/Resources` folder.

## Example

File `app/Http/Resources/V1/ProductResource.php`:

```php
class ProductResource extends JsonResource
{
    public function toArray($request)
    {
        return [
            'id' => $this->id,
            'name' => $this->name,
            'detail' => $this->detail,
            'createdAt' => $this->created_at->format('d/m/Y'),
            'updatedAt' => $this->updated_at->format('d/m/Y'),
        ];
    }
}
```

Notice that we can access model properties directly from the `$this` variable. 
This is because a resource class will automatically 
proxy property and method access down to the underlying model for convenient access.

Controller `app/Http/Controllers/Api/V1/CustomerController.php`:

```php
public function show(Product $product)
{
    return new ProductResource($product);
}
```

File `routes/api.php`:

```php
Route::group(['prefix' => 'v1', 'namespace' => '\App\Http\Controllers\Api\V1'], function() {
   Route::apiResource('products', ProductController::class);
});
```
