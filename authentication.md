# Authentication

Laravel's authentication facilities are made up of:

1. *Guards*. They define how users are authenticated for each request. `session` guard maintains state using session storage and cookies.
2. *Providers*. They define how users are retrieved from your persistent storage. Laravel ships with support for retrieving users using Eloquent 
    and the database query builder.

**Note**: Guards and providers should not be confused with "roles" and "permissions". 
To learn more about authorizing user actions via permissions, please refer to the [authorization](https://laravel.com/docs/master/authorization) documentation.

Config file: `config/auth.php`.

Sessions are stored at `/storage/framework/sessions/3c3DB8KKWMcOHmRNI8CPANl8Apsb55MRsSb741mO`
