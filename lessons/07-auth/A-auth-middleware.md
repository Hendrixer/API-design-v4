We don't want just anyone using our API. Our DB is multi-tenat, so we need to identify what user is making the request so we can scope their queries and writes to the user. We don't want one user having access to another user's data.
<br>
To ensure all of this, we're going to protect our API. Tokens are a great approach for this. Things like API Keys and JWT's are good examples of tokens. You could also use Sessions. We're going to use JWTs.

## Creating a JWT

Lets create a function that create's JWTs for when a new user signups up or current one signs in. Users will need to send the JWT on every single request to get access to the API. Our API never stores a JWT, its stored client side.
<br>

We need to install a few things:

<br>

`npm i jsonwebtoken bcrypt dotenv`
<br>

Create a new file `src/modules/auth` and add this:

```ts
import jwt from "jsonwebtoken";

export const createJWT = (user) => {
  const token = jwt.sign(
    { id: user.id, username: user.username },
    process.env.JWT_SECRET
  );
  return token;
};
```

This function will take a user and create a JWT from the user's id and username. This is helpful for later when we check for a JWT, we then will know what user is making the request.
<br>
To do that check, we'll create custom middleware.

```ts
export const protect = (req, res, next) => {
  const bearer = req.headers.authorization;

  if (!bearer) {
    res.status(401);
    res.send("Not authorized");
    return;
  }

  const [, token] = bearer.split(" ");
  if (!token) {
    console.log("here");
    res.status(401);
    res.send("Not authorized");
    return;
  }

  try {
    const payload = jwt.verify(token, process.env.JWT_SECRET);
    req.user = payload;
    console.log(payload);
    next();
    return;
  } catch (e) {
    console.error(e);
    res.status(401);
    res.send("Not authorized");
    return;
  }
};
```

This middleware functions checks for a JWT on the `Authorization` header of a request. It then attaches the user to the request object before moving on. If anything fails, the user is sent a 401.
<br>
We need to update our `.env` file to have a `JWT_SECRET`. You don't want this secret in your code because it's needed to sign and verify tokens. You can place whatever value you want. Then we need to load in the env file into our environment.
<br>
Inside of `src/index.ts`:

```ts
import * as dotenv from "dotenv";
dotenv.config();
```

This will load in our env vars into the process.

<br>
Lastly, we need to add our middleware onto our API router to protect it, so inside of `src/server.ts`, import protect and add it to the chain:

```ts
app.use("/api", protect, router);
```

Now any API call to anthing `/api` will need to have a JWT.
<br>
Next we'll create some routes and handlers to create users that are issued JWTs.
