As your API gets bigger, it's harder to keep track of things like secrets, options, env vars, etc., especially across different environments. We need want to be able to give our app the flexibility to adapt to each environment (local, staging, prod, etc) without having to change too much. It would be awesome, if everything we needed to change was in one place that we could import everywhere.

## NODE_ENV

Environment variables are values provided from the environment at run time. They're perfect for injecting secret values your server needs, but are too dangerous to store in git.
<br>
One very important env var is `NODE_ENV`. This env var is usually tasked with determining the "mode" your app is running. Some examples are:

- `development` (default)
- `production`
- `testing`

<br>

Some packages like `React` behave differently, depending on the value of this env var. We may also want our code to use different values as well. For instance, if we have analytics on our API, we probably don't want to have that enabled while we're developing locally. So we can check the `NODE_ENV` to see what env we are in and conditionally track based on the environment.
<br>
This is very powerful! However, having a bunch of the same conditionals sprinkled across our app can make it tough when we need to make changes. That's why we're going to centralized all the dynamic values of our app that depend on the current env. This way, we only have to change one file to completely change how our app works.
