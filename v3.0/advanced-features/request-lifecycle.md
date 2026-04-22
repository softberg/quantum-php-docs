# Request Lifecycle

The Quantum PHP Framework becomes much easier to reason about once you understand the full request lifecycle.

This page explains what happens from the moment a request enters the application until a response is returned.

## Why this matters

People often learn routing, controllers, and views as separate topics.
That helps at first, but real confidence comes from understanding how those parts connect.

The request lifecycle is that connection.

## High-level flow

A simple view of the flow looks like this:

1. a request enters the application
2. Quantum boots the required framework pieces
3. the router matches the request
4. route middleware runs
5. the controller action is dispatched
6. the response is prepared
7. output is returned to the client

This is the backbone of nearly every web interaction in the framework.

## 1. The request enters the application

Every HTTP request starts from the public entry point of the app.

At this stage, Quantum needs to:

- load configuration
- bootstrap the container and shared services
- prepare request and response objects
- initialize the routing flow

You can think of this as the framework preparing the execution environment.

## 2. The router tries to match the request

Once the application is ready, Quantum checks the request against the registered routes.

The router is responsible for figuring out:

- which route matches the URL
- which HTTP method is allowed
- which controller and action should handle the request
- which middleware is attached

If no route matches, the request usually ends in a not found response.

## 3. The matched route carries metadata

A matched route is more than just a URL pattern.

It also carries information such as:

- controller name
- action name
- route parameters
- route name
- middleware definitions

That metadata becomes the instruction set for the next steps.

## 4. Middleware runs before the controller action

If middleware is attached to the route, Quantum runs it before calling the controller action.

Middleware can:

- allow the request to continue
- redirect the request
- return an error response
- validate inputs
- block unauthorized access

This is why middleware belongs in the core flow of the framework.

A request does not always go directly from route to controller.
Sometimes middleware stops it first.

## 5. The controller action is dispatched

If middleware allows the request to continue, Quantum dispatches the target controller action.

At this point, the framework resolves the controller and calls the requested method.

Depending on the controller, this step may include:

- dependency injection
- before/after hooks
- request processing
- business logic
- loading data
- choosing how to respond

This is the point where framework structure meets application logic.

## 6. The controller prepares a response

The controller usually returns one of a few common outputs:

- plain text
- rendered HTML via views
- JSON for API responses
- redirects

That output becomes the response sent back to the browser or client.

## 7. The client receives the final result

After processing is complete, Quantum sends the final response back to the requester.

That might mean:

- a rendered page appears in the browser
- JSON is returned to a frontend app
- the user is redirected to another route
- an error response is shown

## Putting the lifecycle together

A practical summary looks like this:

- the framework boots
- the router finds a route
- middleware checks the request
- the controller handles the work
- a response is returned

If you understand that sequence, many other docs pages become easier immediately.

## Example mental flow

Imagine a user visits `/dashboard`.

A likely flow is:

1. Quantum receives the request
2. the router matches `/dashboard`
3. `Auth` middleware checks whether the user is logged in
4. if allowed, `DashboardController@index` runs
5. the controller loads data and renders a dashboard view
6. the browser receives the HTML response

That is the request lifecycle in action.

## Where people often get confused

A few mistakes are common.

### Confusing routing with execution
Routes describe the destination. They do not do all the work themselves.

### Forgetting middleware in the middle
Many people jump straight from route to controller. In real apps, middleware often sits in between.

### Treating views as independent from controllers
Views are usually part of the response chosen by the controller, not a separate routing destination.

## Related pages

To understand the lifecycle better, read these together:

- [Routing](../core-concepts/routing.md)
- [Controllers](../core-concepts/controllers.md)
- [Views](../core-concepts/views.md)
- [Middleware](../core-concepts/middleware.md)
- [Modules Overview](../modules/overview.md)

Once these pages connect in your head as one flow, the framework stops feeling abstract.
