---
description: "Migrating the DB"
---

## Migrations

Since this is our first time interacting with the DB, we need to run our initial migration to get the DB and our schema in sync. We'll continue to run migrations as we make schema changes to ensure the schema and any data in the DB stay in sync. Before we run a migration, we need to install the prisma client which is the SDK we'll use in our code to interact with the DB. This client is type-safe and based on of our schema. It's actually an NPM package that gets generated on demand to adjust to your schema! Pretty cool.
<br>
`npm i @prisma/client --save`
<br>
Next, lets migrate the DB. Make sure you added your DB connection string to the `.env` file as `DATABASE_URL`. You can find the connection string on render. Be sure to use the external one. Now to run the migration:
<br>
`npx prisma migrate dev --name init`
<br>
This will migrate the DB over to use our schema and then generate the new client for us. This client will be used in our code and is now type-checked against our schema.
