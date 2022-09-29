We can overwrite the default handler with our own custom one.

```ts
app.use((err, req, res, next) => {
  if (err.type === "auth") {
    res.status(401);
    res.json({ message: "nope" });
  }
});
```

This is an example of what a custom error handler might look like. If you use any error reporting service to capture and analyze errors, here is where you want to report your errors. We can even have many custom handlers all doing different things. For example, one might log the error, then another reports it to your reporting service, and the last one actually responds to the request.
<br>
We can augment an error however we see fit before passing it to `next`. This will help our custom handler decide on how to handle the actuall error.

```ts
catch (e) {
  e.type = 'input'
  next(e)
}

app.use((err, req, res, next) => {
  if (err.type === 'input') {
    res.status(400)
    return res.send('invalid input')
  }
})
```

## Handle our errors

Next, lets go through our handlers and middleware and make sure we're handling our errors. Also, we must create our own error handler for the app.
