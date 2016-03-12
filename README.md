# What is ui-router?

## Overview

`ngRoute` provides us with basic functionality, but the leading router for Angular is `uiRouter`. This provides much more, such as nested views, multiple views and a few different offerings. Let's take a look at how `uiRouter` does things instead.

## Objectives

- Describe ui-router and ui-view
- Write a route using ui-router
- Integrate a Controller with ui-router
- Integrate a template with ui-router

## uiRouter

`uiRouter` is quite similar to `ngRoute`, but each "route" is known as a "state". We define states, not routes.

Each state that we define is quite similar to a route in `ngRoute`, but we have to give each state a name too. This allows us to have children states inside of a state.

Let's take a look at how we'd define a route in `ngRoute`:

```js
angular
	.module('app', ['ngRoute'])
	.config(function ($routeProvider) {
		$routeProvider
			.when('/user', {
				templateUrl: 'views/user.html',
				controller: 'UserController'
			});
	});
```

And how we'd define a route in `uiRouter`:

```js
angular
	.module('app', ['ui.router'])
	.config(function ($stateProvider) {
		$stateProvider
			.state('user', {
				url: '/user',
				templateUrl: 'views/user.html',
				controller: 'UserController'
			});
	});
```

You can see they're very similar. We've moved the URL into the configuration object, and replaced the URL with the state's name. We're also using `$stateProvider` instead of `$routeProvider`.

Instead of using `ng-view`, we use `ui-view` to place the states in our HTML.

We'll go into more advanced concepts with `uiRouter` soon - things such as nested views and resolving data.

## uiSref

`uiRouter` also provides a directive named `ui-sref`. We can use this on our hyperlinks to generate links to our states. We pass in the state name as the value and `uiRouter` will replace the link with a link to our state.

Say we've got a state named `docs`, that links to `/documentation/v1`:

```js
angular
	.module('app', ['ui.router'])
	.config(function ($stateProvider) {
		$stateProvider
			.state('docs', {
				url: '/documentation/v1',
				templateUrl: 'views/user.html',
				controller: 'UserController'
			});
	});
```

We can then use `ui-sref="docs"` to link to that state.

```html
<a href="" ui-sref="docs">Go to the docs!</a>
```

This will then get automatically changed into:

```html
<a href="/documentation/v1">Go to the docs!</a>
```

This is awesome - we can change the URL on our states without changing the name and all of our links get updated to match the new URL.

## uiSrefActive

`uiRouter` also provides us with one more directive - `ui-sref-active`. We pass in a class name as the value, and when the given state inside our `ui-sref` is active, it will apply this class to the link.

For instance, if we have this:

```html
<a href="" ui-sref="docs" ui-sref-active="active">Go to the docs!</a>
```

When we're actually on the docs page, that link will get the `active` class applied to it:

```html
<a href="" class="active" ui-sref="docs" ui-sref-active="active">Go to the docs!</a>
```

Simple!