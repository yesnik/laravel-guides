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

### isMethod

```php
public function login(Request $request)
{
    if ($request->isMethod('post')) {
        $validatedData = $request->validate([
            'login' => 'required | max:10',
            'password' => 'required | min:8',
        ]);
        dd($validatedData);
    }

    return view('user/login');
}
```

### validate

```php
public function store(Request $request)
{
    $request->validate([
        'name' => 'required|max:25',
        'detail' => 'required',
        'email' => 'email|nullable|unique:claims',
    ]);

    \App\Product::create($request->all());

    return redirect()->route('products.index')
            ->with('success','Product created successfully.');
}
```

In case of an error this method will do `302 Found` redirect to page to display errors.

We can exclude current object's email from validation:

```php
use Illuminate\Validation\Rule;

public function update(Request $request, $id)
{
    $request->validate([
        'email' => [
            'email',
            'required',
             Rule::unique('claims')->ignore($id),
        ],
    ]);

    // ...
}
```

### Form template with errors

File `user/login.blade.php`:

```blade
<form action="/users/login" method="post">
    <div>
        <input type="text" name="login" placeholder="Login" value="{{ old('login') }}" />

        @error('login')
            <p>{{ $message }}</p>
        @enderror
    </div>
    <div>
        <input type="password" name="password" placeholder="Password" value="{{ old('password') }}" />
        @error('password')
            <p>{{ $message }}</p>
        @enderror
    </div>

    <input type="submit" name="Login" />
    @csrf
</form>
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
