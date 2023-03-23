---
description: "Input validation for express requests"
---

Never trust the user! Words to live by when working with user input. Especially more true for an API that is responsible for holding the weight of every client. The last thing you want is for a user's input choice to crash your entire server. We want to get ahead of that and validate all incoming data for our API.
<br>
So what does input validation look like? We'll be using a package to help us do that.
<br>
`npm i express-validator --save`
<br>
For any route, you want to add input validations:

```ts
import { body, validationResult } from "express-validator";

app.post("/product", body("name").isString(), (req, res) => {
  const errors = validationResult(req);

  if (!errors.isEmpty()) {
    res.status(400);
    res.json({ errors: errors.array() });
  }
});
```

We can use the provided middleware to create new validations against any user input. This includes the body, headers, cookies, params, and query string. In this example, we're validating that the request includes a `name` field on the body.
<br>
Let's apply input validations to all our `put` and `post` requests.
