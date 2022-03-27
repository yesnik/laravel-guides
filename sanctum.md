# Laravel Sanctum

See [docs](https://laravel.com/docs/master/sanctum)

It  provides a featherweight authentication system for SPAs (single page applications), mobile applications, 
and simple, token based APIs. Sanctum allows each user of your application to generate multiple API tokens for their account. 
These tokens may be granted abilities / scopes which specify which actions the tokens are allowed to perform.

Laravel Sanctum exists to solve two separate problems.

## API tokens

First, Sanctum is a simple package you may use to issue API tokens to your users without the complication of OAuth. 
Laravel Sanctum stores user API tokens in a single database table and authenticate 
incoming HTTP requests via the `Authorization` header which should contain a valid API token.

## SPA Authentication

Second, Sanctum exists to offer a simple way to authenticate single page applications (SPAs) that need to communicate with a Laravel powered API. 
Sanctum uses Laravel's built-in cookie based session authentication services. 
Typically, Sanctum utilizes Laravel's `web` authentication guard to accomplish this. 
This provides the benefits of CSRF protection, session authentication, as well as protects against leakage of the authentication credentials via XSS.

Sanctum will only attempt to authenticate using cookies when the incoming request originates from your own SPA frontend. 
When Sanctum examines an incoming HTTP request, it will first check for an authentication cookie and, if none is present, 
Sanctum will then examine the `Authorization` header for a valid API token.

## Installation

The most recent versions of Laravel already include Laravel Sanctum.
