---
title: JavaScript
sidebar_order: 7
---

Raven.js is the official browser JavaScript client for Sentry. It automatically reports uncaught JavaScript exceptions triggered from a browser environment, and provides a rich API for reporting your own errors.

**Note**: If you’re using Node.js on the server, you’ll need [raven-node]({%- link _documentation/clients/node/index.md -%}).

## Installation

The easiest way to load Raven.js is to load it directly from our CDN. This script tag should be included after other libraries are loaded, but before your main application code (e.g. app.js):

```html
<script src="https://cdn.ravenjs.com/3.26.4/raven.min.js" crossorigin="anonymous"></script>
```

For installation using npm or other package managers, see [_Installation_]({%- link _documentation/clients/javascript/install.md -%}).

## Configuring the Client

Next you need to configure Raven.js to use your [Sentry DSN]({%- link _documentation/learn/quickstart.md -%}#configure-the-dsn):

```javascript
Raven.config('___PUBLIC_DSN___').install()
```

It is additionally recommended (but not required) to wrap your application start using _Raven.context_. This can help surface additional errors in some execution contexts.

```javascript
Raven.context(function () {
    initMyApp();
});
```

At this point, Raven is ready to capture any uncaught exception.

Once you have Raven up and running, it is highly recommended to check out [_Configuration_]({%- link _documentation/clients/javascript/config.md -%}) and [_Usage_]({%- link _documentation/clients/javascript/usage.md -%}).

## Manually Reporting Errors

By default, Raven makes a best effort to capture any uncaught exception.

To report errors manually, wrap potentially problematic code with a `try...catch` block and call `Raven.captureException`:

```javascript
try {
    doSomething(a[0])
} catch(e) {
    Raven.captureException(e)
}
```

There are more ways to report errors. For a complete guide on this see [Reporting Errors Correctly]({%- link _documentation/clients/javascript/usage.md -%}#raven-js-reporting-errors).

## Adding Context

While a user is logged in, you can tell Sentry to associate errors with user data. This data is then submitted with each error which allows you to figure out which users are affected.

```javascript
Raven.setUserContext({
    email: 'matt@example.com',
    id: '123'
})
```

If at any point, the user becomes unauthenticated, you can call `Raven.setUserContext()` with no arguments to remove their data.

Other similar methods are `Raven.setExtraContext` and `Raven.setTagsContext` as well as `Raven.context`. See [Passing Additional Data]({%- link _documentation/clients/javascript/usage.md -%}#raven-js-additional-context) for more info.

## Breadcrumbs

Breadcrumbs are browser and application lifecycle events that are helpful in understanding the state of the application leading up to a crash.

By default, Raven.js instruments browser built-ins and DOM events to automatically collect a few useful breadcrumbs for you:

> -   XMLHttpRequests
> -   URL / address bar changes
> -   UI clicks and keypress DOM events
> -   console log statements
> -   previous errors

You can also record your own breadcrumbs. For more information, see [Recording Breadcrumbs]({%- link _documentation/clients/javascript/usage.md -%}#raven-js-recording-breadcrumbs).

## Dealing with Minified Source Code

Raven and Sentry support [Source Maps](http://www.html5rocks.com/en/tutorials/developertools/sourcemaps/). If you provide source maps in addition to your minified files that data becomes available in Sentry. For more information see [Source Maps]({%- link _documentation/clients/javascript/sourcemaps.md -%}#raven-js-sourcemaps).

## Browser Compatibility

Raven.js supports all major browsers. In older browsers, error reports collected by Raven.js may have a degraded level of detail – for example, missing stack trace data or missing source code column numbers.

The table below describes what features are available in each supported browser:

| Browser | Line numbers | Column numbers | Stack trace |
| --- | --- | --- | --- |
| Chrome | ✓ | ✓ | ✓ |
| Firefox | ✓ | ✓ | ✓ |
| Edge | ✓ | ✓ | ✓ |
| IE 11 | ✓ | ✓ | ✓ |
| IE 10 | ✓ | ✓ | ✓ |
| IE 9 | ✓ | ✓ |   |
| IE 8 | ✓ |   |   |
| Safari 6+ | ✓ | ✓ | ✓ |
| iOS Safari 6+ | ✓ | ✓ | ✓ |
| Opera 15+ | ✓ | ✓ | ✓ |
| Android Browser 4.4 | ✓ | ✓ | ✓ |
| Android Browser 4 - 4.3 | ✓ |   |   |

For browsers with Web Worker support, Raven.js is designed to work inside a Web Worker context.

For unlisted browsers (e.g. IE7), Raven.js is designed to fail gracefully. Including it on your page should have no effect on your page; it will just not collect and report uncaught exceptions.

## Deep Dive

For more detailed information about how to get most out of Raven.js there is additional documentation available that covers all the rest:

-   [Installation]({%- link _documentation/clients/javascript/install.md -%})
-   [Configuration]({%- link _documentation/clients/javascript/config.md -%})
-   [Usage]({%- link _documentation/clients/javascript/usage.md -%})
-   [Integrations]({%- link _documentation/clients/javascript/integrations/index.md -%})
    -   [AngularJS]({%- link _documentation/clients/javascript/integrations/angularjs.md -%})
    -   [Angular]({%- link _documentation/clients/javascript/integrations/angular.md -%})
    -   [Backbone]({%- link _documentation/clients/javascript/integrations/backbone.md -%})
    -   [Ember]({%- link _documentation/clients/javascript/integrations/ember.md -%})
    -   [React]({%- link _documentation/clients/javascript/integrations/react.md -%})
    -   [Vue.js (2.0)]({%- link _documentation/clients/javascript/integrations/vue.md -%})
-   [Source Maps]({%- link _documentation/clients/javascript/sourcemaps.md -%})
-   [Tips and Tricks]({%- link _documentation/clients/javascript/tips.md -%})

Resources:

-   [Downloads and CDN](http://ravenjs.com/)
-   [Bug Tracker](http://github.com/getsentry/raven-js/issues)
-   [Github Project](http://github.com/getsentry/raven-js)