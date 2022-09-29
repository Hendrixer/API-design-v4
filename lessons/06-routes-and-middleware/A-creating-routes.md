Now that we have our schema and data models, we can start creating routes and route handlers to interact with those models. We'll be following a mostly RESTful approach to our API design, but as you'll soon learn, nothing ever stays the course when it comes to REST.

## Thinking of Routes

Until some other need presents itself, we want to create a route for every CRUD action for every resource. So, in the case of a Product, we want to create:

- `GET product/:id` - get a product by a given ID
- `GET product` - get all the products (for an authenticated user)
- `POST product` - create a new product
- `PUT product/:id` - update or replace a product that matches a given ID
- `DELETE product/:id` - delete a product by a give ID

This is how REST looks. However, when developing an API that's consumed only by a client that you and your team also created, using something like REST is probably redundant and tedious. There's nothing stopping you from just creating an API route to get all the data for every page, or every component, or whatever makes sense for your application. Something like REST is great for external APIs so external developers can onboard more quickly because they know what to expect vs. having to learn some custom API design.

## Create our routes

Create a new file, `src/router.ts` and work in there.

```ts
import { Router } from "express";

const router = Router();
/**
 * Product
 */
router.get("/product", (req, res) => {
  res.json({ message: "product" });
});

router.get("/product/:id", (req, res) => {});

router.post("/product", (req, res) => {});

router.put("/product/:id", (req, res) => {});

router.delete("/product/:id", (req, res) => {});

/**
 * Update
 */

router.get("/update", (req, res) => {});

router.get("/update/:id", (req, res) => {});

router.post("/update", (req, res) => {});

router.put("/update/:id", (req, res) => {});

router.delete("/update/:id", (req, res) => {});

/**
 * UpdatePoint
 */

router.get("/updatepoint", (req, res) => {});

router.get("/updatepoint/:id", (req, res) => {});

router.post("/updatepoint", (req, res) => {});

router.put("/updatepoint/:id", (req, res) => {});

router.delete("/updatepoint/:id", (req, res) => {});

export default router;
```

There are a few things going on here. First we created a new router using Express. This gives us more flexibility around configuring a set of routes vs. the whole API. You can create as many routers as you'd like with Express and mount them back to the main Express app on the appropriate paths.
<br>
We then created all the routes for the DB resources we want to interact with. User is noticiably missing. This is because User will have a special set of routes because of the importantance of that resource. For the handlers, we adding placeholder functions for now. If you try to make an API call, your API will get back a `404` status code and some HTML (default 404 response from Express). That's because we didn't mount this router back to the main Express app. So it's just floating and not actually attached to our API.
Let's do that next:
<br>
head over to `src/server.ts`:

```ts
import router from './router'

.......
app.use('/api', router)
```

Import the router from the other file and remove any current route declerations in `server.ts`. We then use something new here: `app.use()`, this allows you to apply a router or middleware (we will learn about middleware later) to the entire API, or in our case, to anything using the path `/api`. So a route we create in the router like `GET /product`, is now actually `GET /api/product` because the router is mounted on the `/api` path.
<br>
You should now be able to hit your API and not get a 404, but, it still won't work. What's happening now is your API is hanging, which just means it never responded back to the request and there is no more code to execute. The client will eventually timeout and close the connection. This happens because we never send a response in any of the handler functions we created. We'll do that soon, but for now, lets talk about middleware.
