# Horizon

## Useful Articles 

- "Deep Dive into Laravel Horizon — what goes on behind the scenes" - [link](https://medium.com/@zechdc/laravel-horizon-number-of-workers-and-job-execution-order-21b9dbec72d7)
- "Get your application ready for enterprise success with Laravel Queues" - [link](https://www.inspector.dev/what-worked-for-me-using-laravel-queues-from-the-basics-to-horizon/)

## Config

See `config/horizon.php`.

```php
    'environments' => [
        'production' => [
            // ...
        ],

        'local' => [
            'reports' => [
                'connection' => 'redis',
                'queue' => [
                    'reports-high',
                    'reports-medium',
                ],
                'maxProcesses' => 1,
                'balance' => 'false',
                'tries' => 1,
            ],
            'images' => [
                'connection' => 'redis',
                'queue' => ['images-medium'],
                'maxProcesses' => 1,
                'balance' => 'false',
                'tries' => 1,
            ],
        ],
    ],
```

## Job

```php
namespace App\Jobs;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Foundation\Bus\Dispatchable;
use Illuminate\Queue\InteractsWithQueue;
use Illuminate\Queue\SerializesModels;
use Illuminate\Support\Facades\Log;

class CompressImage implements ShouldQueue
{
    use Dispatchable, InteractsWithQueue, Queueable, SerializesModels;

    /**
     * The number of seconds the job can run before timing out.
     *
     * @var int
     */
    public $timeout = 70;

    /**
     * @var string
     */
    private $imageType;

    /**
     * Create a new job instance.
     *
     * @return void
     */
    public function __construct(string $imageType)
    {
        $this->imageType = $imageType;
    }

    /**
     * Execute the job.
     *
     * @return void
     */
    public function handle()
    {
        sleep(62);
        Log::info('Image type: ' . $this->imageType);
    }
}
```

### `$timeout`

By default job has `$timeout = 60`. If job executes too long Laravel will throw an error: 
"Illuminate\Queue\MaxAttemptsExceededException: App\Jobs\CompressImage has been attempted too many times or run too long. The job may have previously timed out."
Executed job will be killed during the process.
