Let's create a new file `src/config/index.ts`. Then, for every environment, we'll create a file. Those enviroments are local, staging, and production.
<br>
<br>

So create, `src/config/local.ts`, `src/config/staging.ts`, `src/config/prod.ts`. Each of one these files will be used to configure variables for their matching environment.

<br>
Next, we'll merge the configs together, giving us our final config that we can use anywhere.
<br>
In `src/config/index.ts`

```ts
import merge from "lodash.merge";

// make sure NODE_ENV is set
process.env.NODE_ENV = process.env.NODE_ENV || "development";

const stage = process.env.STAGE || "local";
let envConfig;

// dynamically require each config depending on the stage we're in
if (stage === "production") {
  envConfig = require("./prod").default;
} else if (stage === "staging") {
  envConfig = require("./staging").default;
} else {
  envConfig = require("./local").default;
}

const defaultConfig = {
  stage,
  dbUrl: process.env.DATABASE_URL,
  jwtSecret: process.env.JWT_SECRET,
  port: process.env.PORT,
  logging: false,
};

export default merge(defaultConfig, envConfig);
```
