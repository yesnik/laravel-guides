# Models

## Console commands

```bash
# Create model with migration and controller
php artisan make:model Post -mc

# Create model with:
# Model app/Models/Customer.php 
# Factory database/factories/CustomerFactory.php
# Migration database/migrations/2022_12_25_015743_create_customers_table.php 
# Seeder database/seeders/CustomerSeeder.php
# Request app/Http/Requests/StoreCustomerRequest.php 
# Request app/Http/Requests/UpdateCustomerRequest.php 
# Controller app/Http/Controllers/CustomerController.php 
# Policy app/Policies/CustomerPolicy.php
php artisan make:model Customer --all
```

## Eloquent ORM methods

```php
Post::all();
Tag::all()->pluck('name')->toArray(); // ['php', 'python', 'ruby']

Post::latest()->get(); // ORDER BY created_at DESC
Post::latest('updated_at')->get(); // ORDER BY updated_at DESC

Post::first();
Post::firstOrFail();
Post::find(15); // WHERE id = 15

Post::take(2)->get();
Post::take(3)->latest()->get();

Post::where('published', true)->get();
Post::where('created_at', '>=', '2019-06-01')->get()->count();

$user = User::find(1);
$posts = $user->posts()->get();

$post = Post::firstOrCreate(['name' => 'War and Peace']);
$post = Post::firstOrNew(['name' => 'War and Peace']);
$post = Post::updateOrCreate(['name' => 'War and Peace']);

Post::where('active', 0)->delete();
$post = Post::find(1);
$post->delete();

DB::select('select * from users');
```

## Example of the model

File `app/Article.php`:

```php
class Article extends Model
{
    use HasFactory;

    // Mass assignment allowed for these attributes
    protected $fillable = ['title', 'excerpt', 'body'];
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
## Relations

### hasMany / belongsTo

```php
$user = App\User::find(1);
$user->articles;

$article = App\Article::find(5);
$article->user;
```

It's possible because we defined methods:

```php
class Article extends Model
{
    public function user()
    {
        return $this->belongsTo(User::class)->orderBy('created_at');
    }
}
```

```php
class User extends Authenticatable
{
    // ...
    public function articles()
    {
        return $this->hasMany(Article::class);
    }
}
```

### belongsToMany

```php
class Article extends Model
{
    public function tags()
    {
        return $this->belongsToMany(Tag::class);
    }
}

class Tag extends Model
{
    public function articles()
    {
        return $this->belongsToMany(Article::class);
    }
}
```

To organize many-to-many relationship we need to create linking table `article_tag`.
It will allow us to do this:

```php
$article = App\Article::find(1);
$article->tags;

$tag = App\Tag::first();
$tag->articles;
```
