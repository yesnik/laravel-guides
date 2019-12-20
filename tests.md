# Tests in Laravel

Laravel supports 2 types of tests:

- Feature tests: controllers
- Unit tests: models

## Console command

Generate feature test

```bash
php artisan make:test Http/Controllers/ClaimControllerTest
```
It will create file: `tests/Feature/Http/Controllers/ClaimControllerTest.php`

## Feature tests

See documentation for [HTTP Tests](https://laravel.com/docs/master/http-tests)
