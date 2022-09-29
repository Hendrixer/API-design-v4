If an error is not caught on our server, it will crash and our API will non function.
To avoid this, we want to make sure we catch any and all potential errors. We also want to do right by the requester and inform them on any errors, especially if it's their fault. Express uses it's middleware system to ship a default error handler that does a good job at catching any syncronous errors that throw inside middleware and handlers. Let's test that:

```ts
app.get("/", () => {
  throw new Error("oops");
});
```

If you were to run this, you will see an error in your terminal, however, the server would not have crashed. Express is adding a default error handler to the complete bottom of our router stack. Error handling middleware are just like all middleware except they don't run before a handler, they only run after an error has been thrown.

```ts
app.use((err, req, res, next) => {
  // handle error
});
```

As long as your error handler is registered last, it wull catch errors. Now, what about async errors? Well, we have to tell express about our async errors. Inside our handlers and middleware:

```ts
const handler = async (req, res, next) = {
  // ....
  try {
    const user = await prisma.user.create({})
  } catch(e) {
    next(e)
  }
}
```

Anything we pass to `next` is considered an error.
