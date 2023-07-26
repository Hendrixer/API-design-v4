We know from our schema that a user needs a unique username and password. Lets create a handler to create a user. Before we can do that, we'll create some helper functions to hash and compare a user's password so we're not storing it in plain text.
<br>
Inside of `src/modules/auth.ts`

```ts
import * as bcrypt from "bcrypt";

export const comparePasswords = (password, hash) => {
  return bcrypt.compare(password, hash);
};

export const hashPassword = (password) => {
  return bcrypt.hash(password, 5);
};
```

`comparePasswords` compare a plain text password and hashed password to see if they're the same.
<br>

`hashPassword` hashes a password.
<br>
Now, let's create that handler inside `src/handlers/user.ts`

```ts
import prisma from "../db";
import { createJWT, hashPassword } from "../modules/auth";

export const createNewUser = async (req, res) => {
  const hash = await hashPassword(req.body.password);

  const user = await prisma.user.create({
    data: {
      username: req.body.username,
      password: hash,
    },
  });

  const token = createJWT(user);
  res.json({ token });
};
```

First thing here is the prisma import. I'm creating module that exports a Prisma client so we don't have to keep creating a new client every time we need it.
<br>
There isn't anything special going on here other than creating a new user then using that user to create a JWT and sending that token back as a response.
<br>
Next, we need to allow a user to sign in.

```ts
export const signin = async (req, res) => {
  const user = await prisma.user.findUnique({
    where: { username: req.body.username },
  });

  const isValid = await comparePasswords(req.body.password, user.password);

  if (!isValid) {
    res.status(401);
    res.send("Invalid username or password");
    return;
  }

  const token = createJWT(user);
  res.json({ token });
};
```

Using the provided username, we search for a matching user. We'll get more into how to query with Prisma soon. Then we compare passwords. If it's a match, we create a JWT and send it back.

<br>
Now we need to create some routes and add these handlers. We can do this in `src/server.ts`

```ts
import { createNewUser, signin } from "./handlers/user";

app.post("/user", createNewUser);
app.post("/signin", signin);
```
