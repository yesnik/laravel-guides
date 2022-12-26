# API Resources

See [documentation](https://laravel.com/docs/master/eloquent-resources)

When building an API, you may need a transformation layer that sits between your 
Eloquent models and the JSON responses that are actually returned to your application's users.

API resources are made of 2 entities: 

- *resource class*. We use it to transform a *single* model to JSON.
- *resource collection*. We use it to transform *collection* of models to JSON.

## Console commands

```bash
# Create a resource class
php artisan make:resource V1\\ProductResource

# Create a resource collection
php artisan make:resource V1\\ProductCollection
```
Files will be created at `app/Http/Resources/V1` folder.

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

### Controller

Controller `app/Http/Controllers/Api/V1/ProductController.php`:

**Single model**

```php
public function show(Product $product)
{
    return new ProductResource($product);
}
```

**Collection of models**

```php
public function index()
{
    return new ProductCollection(Product::paginate());
}
```

The collection of items will be paginated.

### Router

File `routes/api.php`:

```php
Route::group(['prefix' => 'v1', 'namespace' => '\App\Http\Controllers\Api\V1'], function() {
   Route::apiResource('products', ProductController::class);
});
```
