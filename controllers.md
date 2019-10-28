# Controllers

## Render view

```php
// app/Http/Controllers/PostsController.php

namespace App\Http\Controllers;

class PostsController extends Controller
{
    public function show($slug)
    {
        $post = \DB::table('posts')->where('slug', $slug)->first();

        return view('posts/show', [
            'post' => $post,
        ]);
    }
}
```
View is located here: `resources/views/posts/show.blade.php`
