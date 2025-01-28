# Migrations

## Console commands

```bash
# Create a migration
php artisan make:migration add_user_id_to_articles_table
php artisan make:migration create_posts_table
```

```bash
# Apply migrations
php artisan migrate
```

```bash
# Rollback one latest migration
php artisan migrate:rollback
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
    $table->dateTime('checked_at')->nullable();
    
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
    // Way 1
    $table->foreignId('user_id')->constrained()->cascadeOnUpdate()->cascadeOnDelete();
    
    // Way 2
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

### Add fulltext index

```php
Schema::create('posts', function (Blueprint $table) {
    $table->text('body')->fulltext();
});
```

This migration will create *Full text* index for column `body`.

Use this code to use `MATCH AGAINST` query:

```php
Post::whereFullText('body', 'occaecati')->count()
```
