# Forms

## Form example

We need to include `@csrf` in the form.
If we use PUT, DELETE HTTP-methods we need to use `@method('PUT')`

File `resources/views/articles/edit.blade.php`:

```blade
<form method="POST" action="/articles/{{ $article->id }}">
    @csrf
    @method('PUT')

    <input class="{{ $errors->has('title') ? 'is-danger' : '' }}" type="text" name="title">
    
    @error('title')
        <p class="help is-danger">{{ $errors->first('title') }}</p>
    @enderror
    <button type="submit">Submit</button>
</form>
```