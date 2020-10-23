# Logging

## Log message

```php
use use Illuminate\Support\Facades\Log;

Log::info('Product created');
Log::error('Some error');
```

Messages will be logged to `storage/logs/laravel.log`

## Config

See `.env` for activated logging channel:

```
LOG_CHANNEL=stack
```

At `config/logging.php` we can find available channels:

```php 
    'channels' => [
        'stack' => [
            'driver' => 'stack',
            'channels' => ['single'],
            'ignore_exceptions' => false,
        ],

        'single' => [
            'driver' => 'single',
            'path' => storage_path('logs/laravel.log'),
            'level' => env('LOG_LEVEL', 'debug'),
        ],
        // ...
```

**Note:** `stack` is a channel that can accumulate messages from other channels.
