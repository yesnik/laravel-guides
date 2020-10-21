# Notifications

## Create notification

```bash
php artisan make:notification InvoicePaid
```

File `app/Notifications/InvoicePaid.php` will be created.

## Send notification

1. Via `notify` method of the `Notifiable` trait

```php
use App\Notifications\InvoicePaid;

$user = User::find(1);
$user->notify(new InvoicePaid($invoice));
```

2. Via `Notification` facade

```php
Notification::send($users, new InvoicePaid($invoice));
```

## Queueing Notifications

Just add interface to notification's class:

```php
use Illuminate\Contracts\Queue\ShouldQueue;

class InvoicePaid extends Notification implements ShouldQueue
{
    use Queueable;

    // ...
}
```

Run worker to process queued jobs:

```php
php artisan queue:work
```
