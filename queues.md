# Queues

## Console commands

- `php artisan make:job HelloJob` - file `app/Jobs/HelloJob.php` will be created
- `php artisan job:failed` - list all failed jobs. They are from a table `failed_jobs`
- `php artisan job:retry 150` - retry failed job that has id = 150 in the table `failed_jobs`
- `php artisan job:retry all` - retry all failed jobs
- `php artisan queue:flush` - flush all failed jobs. Table `failed_jobs` will be cleared

## Class Structure

Job classes are very simple, normally containing only a `handle` method which is called when the job is processed by the queue. 

```php
namespace App\Jobs;
 
use App\Podcast;
use App\AudioProcessor;
use Illuminate\Bus\Queueable;
use Illuminate\Queue\SerializesModels;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;
 
class ProcessPodcast implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;
 
    protected $podcast;

    public function __construct(Podcast $podcast)
    {
        $this->podcast = $podcast;
    }

    public function handle(AudioProcessor $processor)
    {
        // Process uploaded podcast...
    }
}
```

## Dispatching Jobs

```php
ProcessPodcast::dispatch($podcast);
```
```php
// Delayed dispatch:
ProcessPodcast::dispatch($podcast)
    ->delay(now()->addMinutes(10));
```
```php
// Push job to a queue:
ProcessPodcast::dispatch($podcast)->onQueue('processing');
```

## Job's params

### Max Attempts

To specify the maximum number of times a job may be attempted is via the `--tries`:

```
php artisan queue:work --tries=3
```

### Timeout

The maximum number of seconds that jobs can run may be specified using the `--timeout`:

```
php artisan queue:work --timeout=10
```

