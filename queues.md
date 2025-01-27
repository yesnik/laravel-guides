# Queues

## Console commands

- `php artisan make:job HelloJob` - file `app/Jobs/HelloJob.php` will be created
- `php artisan job:failed` - list all failed jobs. They are from a table `failed_jobs`
- `php artisan job:retry 150` - retry failed job that has id = 150 in the table `failed_jobs`
- `php artisan job:retry all` - retry all failed jobs
- `php artisan queue:flush` - flush all failed jobs. Table `failed_jobs` will be cleared
