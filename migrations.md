# Migrations

## Examples of migrations

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
