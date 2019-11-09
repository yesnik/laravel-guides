# Forms

## Form example

We need to include `@csrf` in the form.
If we use PUT, DELETE HTTP-methods we need to use `@method('PUT')`

File `resources/views/articles/edit.blade.php`:

```blade
<form method="POST" action="/articles/{{ $article->id }}">
    @csrf
    @method('PUT')

    <input type="text" name="title" value="{{ $article->title }}">
    <button type="submit">Submit</button>
</form>
```
