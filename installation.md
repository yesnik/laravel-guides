# Installation

1. Download Laravel installer:

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
Laravel Installer 4.0.5
```

4. Create new project:

```bash
laravel new mysite
```
