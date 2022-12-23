# Files

See [docs](https://laravel.com/docs/master/requests#files)

## Example

View `upload.blade.php`:

```blade
<form action="/upload" method="post" enctype="multipart/form-data">
    @csrf
    <input type="file" name="document[]"><br>
    <input type="file" name="document[]"><br>
    <input type="submit">
</form>
```

Controller:

```php
public function upload(Request $request)
{
    $document = $request->file('document');
    if (is_array($document)) {
        foreach ($document as $item) {
            $item->store('docs');
        }
    } else {
        $document->store('docs');
    }

    // ...
}
```

Files will be saved to `storage/app/docs` with arbitrary name like this `m9KSluayr8n8tHD9MqJAlRg2kD99HH8nFcL821Pt.png`

### Save with original file name

The file will be saved with the original file name. Edit controller's action:

```php
$document = $request->file('document');

$document->storeAs('docs', $document->getClientOriginalName());
```
