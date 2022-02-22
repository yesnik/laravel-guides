# Migrations

## Console commands

```bash
# Create migration
php artisan make:migration add_user_id_to_articles_table
php artisan make:migration create_posts_table

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
    
    $table->string('slug')->unique();
    $table->text('body');
    $table->boolean('completed')->default(false);
    $table->timestamp('due_date')->nullable();
    $table->date('cancelled_on');
    
    $table->timestamps();
});
```

### Create linking table for ManyToMany relation

```php
Schema::create('article_tag', function (Blueprint $table) {
    $table->bigIncrements('id');
    $table->unsignedBigInteger('article_id');
    $table->unsignedBigInteger('tag_id');
    $table->timestamps();

    $table->unique(['article_id', 'tag_id']);

    $table->foreign('article_id')->references('id')->on('articles');
    $table->foreign('tag_id')->references('id')->on('tags');
});
```

### Add column / Add foreign key

```php
Schema::table('articles', function (Blueprint $table) {
    $table->unsignedBigInteger('user_id')->after('body');
    
    $table->foreign('user_id')->references('id')->on('users');
});
```

Add `user_id` column with foreign key constraint:

```php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->foreignIdFor(\App\Models\User::class)->constrained()->onDelete('cascade');
    $table->string('title');
    $table->text('body');
    $table->timestamps();
});
```

### Drop column / Drop foreign key

```php
Schema::table('articles', function (Blueprint $table) {
    $table->dropForeign(['user_id']);
    
    $table->dropColumn('user_id');
});
```
