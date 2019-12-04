# Laravel Commands

## Console commands

- `php artisan make:command DeleteOldProducts` - create command at `app/Console/Commands/DeleteOldProducts.php`
- `php artisan app:delete_old_products` - run custom command
- `php artisan schedule:run` - run registered schedule commands

## Command example

File `app/Console/Commands/DeleteOldProducts.php`:

```php
<?php

namespace App\Console\Commands;

use Illuminate\Console\Command;

class DeleteOldProducts extends Command
{
    protected $signature = 'app:delete_old_products';
    protected $description = 'Delete old products';

    public function handle()
    {
        $this->info('Some info');
        $this->error('Some error');

        \Log::info("This will be logged");
        \Log::error("This Error will be logged");
    }
}
```

Log files are stored at folder `storage/logs/`.

### Add command to scheduler

Edit `app/Console/Kernel.php`:

```php
class Kernel extends ConsoleKernel
{
    // ...
    
    protected function schedule(Schedule $schedule)
    {
        $schedule->command('command:delete_old_products')
            ->everyMinute();
    }

}

```

See other scheduler [frequency options](https://laravel.com/docs/master/scheduling#schedule-frequency-options):

- `->hourly();`
- `->dailyAt('13:00');`
- `->monthly();`

### Add scheduler to crontab

Edit `crontab` file on your server:

```
* * * * * cd /your-project-folder && php artisan schedule:run >> /dev/null 2>&1
```
