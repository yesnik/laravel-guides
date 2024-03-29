# Tests in Laravel

Laravel supports 2 types of tests:

- Feature tests: controllers
- Unit tests: models

## Console command

**Run tests with coverage**

```bash
XDEBUG_MODE=coverage php artisan test --coverage
XDEBUG_MODE=coverage php artisan test --coverage --min=80
```

**Generate feature test**

```bash
php artisan make:test Http/Controllers/ClaimControllerTest
```
It will create file: `tests/Feature/Http/Controllers/ClaimControllerTest.php`

## Feature tests

See HTTP Tests [documentation](https://laravel.com/docs/master/http-tests)

### Test response 200 and rendered view

```php
use Illuminate\Foundation\Testing\RefreshDatabase;

class ClaimControllerTest extends TestCase
{
    use RefreshDatabase;

    /** @test */
    public function index_returns_claims_list()
    {
        $response = $this->get(route('claims.index'));

        $response->assertStatus(200);
        $response->assertViewIs('claim.index');
    }
}
```

### Test redirect to route, flash message

```php
class ClaimControllerTest extends TestCase
{
    use RefreshDatabase;
    
    /** @test */
    public function store_creates_claim()
    {
        $response = $this->post(route('claims.store'), [
            'first_name' => 'Joe',
        ]);

        $response->assertRedirect(route('claims.index'));
        $response->assertSessionHas('success', 'Claim has been successfully created');
    }
```

## Unit tests

### Create / build model

```php
# Build entity
$claim = factory(Claim::class)->make([
    'first_name' => 'Joe',
]);
$claim->id; // null
$claim->first_name; // 'Joe'

# Create record in database
$claim = factory(Claim::class)->create();
$claim->id; // 1
```

### Useful methods

```php
$this->assertDatabaseHas('claims', [
    'last_name' => 'Johnson',
]);
```

**Check authentication**

```php
$user = User::where('email', $email)->where('name', $name)->first();
$this->assertNotNull($user);

$this->assertAuthenticatedAs($user);
```

**Set authenticated user for request**

```php
/** @test */
public function index_returns_a_view()
{
    $user = factory(User::class)->create();

    $response = $this->actingAs($user)->get(route('home'));

    $response->assertStatus(200);
}
```

### Add faker

```php
class ClaimControllerTest extends TestCase
{
    use WithFaker;
    
    $name = $this->faker->name;
    $email = $this->faker->safeEmail;
    // ...
}
```
