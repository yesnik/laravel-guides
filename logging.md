# Logging

## Log message

```php
use use Illuminate\Support\Facades\Log;

Log::info('Product created');
Log::error('Some error');
```

Messages will be logged to `storage/logs/laravel-2020-10-23.log`

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
            'channels' => ['daily'],
            'ignore_exceptions' => false,
        ],

        'single' => [
            'driver' => 'single',
            'path' => storage_path('logs/laravel.log'),
            'level' => 'debug',
        ],
        // ...
```

**Note:** `stack` is a channel that accumulate messages from other channels.
