# Controllers

## Console commands

```bash
# Create controller with 7 CRUD actions
php artisan make:controller PostsController -r

# Create controller for model
php artisan make:controller ProductController --resource --model=Product
```

## Useful methods

### Get POST / GET params

```php
request()->all();
request('title');
```

### redirect

```php
public function store()
{
    // ...
    
    // Way 1
    return redirect('/articles');
    
    // Way 2
    return redirect()->route('products.index');
}
```

### paginate

```php
public function index()
{
    $claims = \App\Claim::latest()->paginate(30);

    return view('products.index', compact('claims'));
}
```

### validate

```php
public function store(Request $request)
{
    $request->validate([
        'name' => 'required|max:25',
        'detail' => 'required',
        'email' => 'email|nullable',
    ]);

    \App\Product::create($request->all());

    return redirect()->route('products.index')
            ->with('success','Product created successfully.');
}
```

## Render view

```php
// app/Http/Controllers/PostsController.php

namespace App\Http\Controllers;

class PostsController extends Controller
{
    public function show($slug)
    {
        $post = \DB::table('posts')->where('slug', $slug)->first();
        
        if (!$post) {
            abort(404);
        }

        return view('posts.show', [
            'post' => $post,
        ]);
    }
}
```
View is located here: `resources/views/posts/show.blade.php`
