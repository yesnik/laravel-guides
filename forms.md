# Forms

You can use [LaravelCollective/html](https://github.com/LaravelCollective/html) package to work with forms.

## Form example

We need to include `@csrf` in the form.
If we use PUT, DELETE HTTP-methods we need to use `@method('PUT')`

File `resources/views/articles/edit.blade.php`:

```blade
<form method="POST" action="/articles/{{ $article->id }}">
    @csrf
    @method('PUT')

    <input 
        type="text"
        class="{{ $errors->has('title') ? 'is-danger' : '' }}" 
        name="title"
        value="{{ old('title') }}"
    >
    
    @error('title')
        <p class="help is-danger">{{ $errors->first('title') }}</p>
    @enderror
    <button type="submit">Submit</button>
</form>
```

## Form for DELETE

```blade
<form action="{{ route('products.destroy',$product->id) }}" method="POST">
  @csrf

  @method('DELETE')

  <button type="submit">Delete</button>
</form>
```
