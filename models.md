# Models

## Generate model

```bash
php artisan make:model Post

# with migration and controller
php artisan make:model Post -mc
```

## Eloquent ORM methods

```php
App\Post::all();

App\Post::latest()->get(); // ORDER BY created_at DESC
App\Post::latest('updated_at')->get(); // ORDER BY updated_at DESC

App\Post::first();
App\Post::find(15); // WHERE id = 15

App\Post::take(2)->get();
App\Post::take(3)->latest()->get();

App\Post::where('published', true)->get();
```

## Example of the model

File `app/Article.php`:

```php
class Article extends Model
{
    // Mass assignment allowed for these attributes
    protected $fillable = ['title', 'excerpt', 'body'];
    
    // See "Define route key" section on this page
    public function getRouteKey()
    {
        return 'slug';
    }
}

```

## Define route key

File `app/Article.php`:

```php
class Article extends Model
{
    public function getRouteKey()
    {
        return 'slug';
    }
}
```

File `routes/web.php`:

```php
Route::get('/articles/{article}', 'ArticlesController@show');
```

File `app/Http/Controllers/ArticlesController.php`:

```php
class ArticlesController extends Controller
{
    public function show(Article $article)
    {
        // Laravel will find article by "slug"
        return view('articles.show', ['article' => $article]);
    }
}
```
