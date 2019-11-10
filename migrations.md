# Migrations

## Console commands

```bash
# Create migration
php artisan make:migration add_user_id_to_articles_table

# Apply migrations
php artisan migrate

# Rollback one latest migration
php artisan migrate:rollback --step=1
```

## Examples

### Create table

```php
Schema::create('assignments', function (Blueprint $table) {
    $table->bigIncrements('id');
    
    $table->string('slug');
    $table->text('body');
    $table->boolean('completed')->default(false);
    $table->timestamp('due_date')->nullable();
    
    $table->timestamps();
});
```

### Add column / Add foreign key

```php
Schema::table('articles', function (Blueprint $table) {
    $table->unsignedBigInteger('user_id')->after('body');
    
    $table->foreign('user_id')->references('id')->on('users');
});
```

### Drop column / Drop foreign key

```php
Schema::table('articles', function (Blueprint $table) {
    $table->dropForeign(['user_id']);
    
    $table->dropColumn('user_id');
});
```
