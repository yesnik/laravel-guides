# Laravel Scout

Docs: https://laravel.com/docs/master/scout

[Laravel Scout](https://github.com/laravel/scout) provides a simple, driver based solution for adding full-text search to your Eloquent models. 
Using model observers, Scout will automatically keep your search indexes in sync with your Eloquent records.

## Installation

1. Install package:
    ```bash
    composer require laravel/scout
    ```
2. Copy scout's config to our project:
    ```bash
    php artisan vendor:publish
    ```
    Select num related to scout, e.g. `Laravel\Scout\ScoutServiceProvider`. This command will create `config/scout.php`.
3. Edit `.env`:
    ```
    SCOUT_DRIVER=database
    ```
4. Add `Searchable` trait and `toSearchableArray()` method to model:
    ```
    namespace App\Models;

    use Illuminate\Database\Eloquent\Factories\HasFactory;
    use Illuminate\Database\Eloquent\Model;
    use Laravel\Scout\Searchable;

    class Post extends Model
    {
        use HasFactory;
        use Searchable;
        
        public function toSearchableArray()
        {
            return [
                'title' => $this->title,
                'body' => $this->body,
            ];
        }
    }
    ```
5. Search posts with provided phrase:
    ```
    Route::get('/', function () {
        return \App\Models\Post::search('qui ex')->get();
    });
    ```
