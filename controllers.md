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
    return redirect('/articles');
}
```

### paginate

```php
public function index()
{
    return Employee::paginate(10);
}
```
This will return JSON:

```json
{
   "current_page":1,
   "data":[
      {
         "id":1,
         "name":"Christelle Kunze",
         "email":"yschimmel@powlowski.com",
         "start_date":"1986-02-17",
         "due_date":"2005-08-19",
         "created_at":"2019-12-02 09:41:18",
         "updated_at":"2019-12-02 09:41:18"
      }
   ],
   "first_page_url":"http:\/\/127.0.0.1:8000\/api\/employee?page=1",
   "from":1,
   "last_page":5,
   "last_page_url":"http:\/\/127.0.0.1:8000\/api\/employee?page=5",
   "next_page_url":"http:\/\/127.0.0.1:8000\/api\/employee?page=2",
   "path":"http:\/\/127.0.0.1:8000\/api\/employee",
   "per_page":10,
   "prev_page_url":null,
   "to":10,
   "total":50
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
