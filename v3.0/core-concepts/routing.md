# Routing

Routing is the part of the Quantum PHP Framework that decides which code should handle an incoming request.

When a request reaches your application, Quantum matches the request method and URL against the registered routes, then dispatches the matching controller action or closure.

## Core idea

A route answers three basic questions:

- which HTTP method is allowed
- which URL pattern should match
- which handler should run

In Quantum PHP Framework, routes are not defined in one giant global file by default. They are built from module route definitions.

## Where routes live

In the framework's module structure, each module provides its own route file at:

```text
modules/<ModuleName>/routes/routes.php
```

The core module loader reads those route definitions during startup, and the route builder composes them into the application's route collection.

## How Quantum builds routes

From the upstream source, the flow is:

1. modules are loaded during web app startup
2. each enabled module contributes a route closure
3. `RouteBuilder` builds a `RouteCollection`
4. `RouteFinder` matches the current request
5. `RouteDispatcher` runs the matching controller action or closure

That means routing in Quantum is tightly connected to the module system.

## Basic route definitions

Quantum supports common route methods such as:

- `get()`
- `post()`
- `put()`
- `delete()`
- `add()` for multiple methods

A simple route can look like this:

```php
return function ($route) {
    $route->get('/', 'MainController', 'index');
};
```

This means:

- match `GET /`
- run `MainController::index()`

## Multi-method routes

If one endpoint should accept more than one HTTP method, Quantum supports that too:

```php
$route->add('signin', 'GET|POST', 'AuthController', 'signin');
```

This is useful for pages or endpoints that both display and handle a form-like flow.

## Route patterns and parameters

Quantum routes support parameterized patterns.

Examples from the upstream templates include:

```php
$route->get('post/[uuid=:any]', 'PostController', 'post');
$route->get('activate/[token=:any]', 'AuthController', 'activate');
$route->add('verify/[code=:any]?', 'GET|POST', 'AuthController', 'verify');
```

These patterns show that Quantum supports:

- named parameters such as `uuid` and `token`
- typed or constrained pattern segments such as `:any`
- optional segments using `?`

The router also exposes helper functions for current route information, including route parameters.

## Named routes

A route can be given a name:

```php
$route->get('posts', 'PostController', 'posts')->name('posts');
```

Named routes make it easier to refer to important endpoints by intention instead of by repeating raw paths.

## Route groups

Quantum supports grouping related routes:

```php
$route->group('auth', function ($route) {
    $route->get('my-posts', 'PostManagementController', 'myPosts');
    $route->get('signout', 'AuthController', 'signout');
})->middlewares(['Auth']);
```

This is useful when several routes share the same concern, such as authentication.

## Middlewares on routes

A route can have middlewares attached to it:

```php
$route->post('signup', 'AuthController', 'signup')->middlewares(['Signup']);
```

A group can also have middlewares applied to all routes inside it:

```php
$route->group('guest', function ($route) {
    // routes...
})->middlewares(['Guest']);
```

This keeps route files readable while still applying shared request rules.

## Route prefixes and modules

The core routing system stores module and prefix information as part of each route.

That matters because Quantum does not treat routes as isolated strings only. A route can carry structured metadata such as:

- module
- prefix
- group
- middlewares
- cache settings
- name

This gives the routing layer more context than a minimal URL matcher.

## Controller routes and closure routes

Quantum supports both:

- controller-action routes
- closure routes

If a route is closure-based, the dispatcher invokes the closure directly.
If a route uses a controller, the dispatcher instantiates the controller and calls the action method.

## Controller lifecycle hooks

The route dispatcher also supports controller lifecycle hooks:

- `__before`
- `__after`

If those methods exist on the controller, they are called around the main action.

This is useful for setup work such as layout configuration or shared page preparation.

## CSRF-aware controller dispatch

The dispatcher checks whether a controller enables CSRF verification through a `csrfVerification` property.

If that property is enabled and the request method requires verification, Quantum checks the CSRF token before continuing.

That means route dispatch is not only about matching a URL. It also participates in request safety.

## Inspecting routes from the CLI

Quantum includes a route listing command:

```bash
php qt route:list
```

It can also filter by module.

This is helpful when you want to verify what the application has actually registered.

## Practical view

A useful way to think about Quantum routing is:

- each module defines its own routes
- each route maps a method and URL pattern to a handler
- the framework collects those routes at startup
- the router finds the matching route for the request
- the dispatcher runs the controller action or closure

## What to read next

After routing, the next best topic is controllers, because routes usually point to controller actions in real applications.
