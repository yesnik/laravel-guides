# Installation

## Via composer

After we have installed PHP and Composer, we can create a new Laravel project via the Composer and [laravel/laravel](https://packagist.org/packages/laravel/laravel) package:

```
composer create-project laravel/laravel mysite-laravel
```

## Via Laravel Installer

1. Download [Laravel installer](https://github.com/laravel/installer):

```bash
composer global require laravel/installer
```

2. Add to file `~/.bashrc`:

```bash
# Composer
export PATH="$HOME/.config/composer/vendor/bin:$PATH"
```

3. Restart console window. Check installation:

```bash
laravel --version
# Laravel Installer 4.2.10
```

4. Create new project:

```bash
laravel new mysite
```

5. Create `.env` and define database credentials:

```bash
cp .env.example .env
vim .env
```

6. Generate application key:

```bash
php artisan key:generate
```

7. Run development server:

```bash
php artisan serve
```
