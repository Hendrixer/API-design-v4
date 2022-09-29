---
description: "Creating DB models with with Primsa"
---

## Prisma Syntax

Prisma has an easy to understand syntax for creating models. Its based on the GraphQL language which is based on JSON. So you'll feel right at home. I highly recommend installing the Prisma VS Code plugin. It lints and cleans up your schema file.

<br>
Now, onto the models. Let's look at an example model.
<br>

```prisma
model Post {
  // id field that is a number and automatically increments after its used
  id        Int      @id @default(autoincrement())
  // timestamps
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  // limit to 255 for indexing UTF-8
  title     String   @db.VarChar(255)
  // optional
  content   String?
  published Boolean  @default(false)
  // relation to another model
  author    User     @relation(fields: [authorId], references: [id])
  authorId  Int
}
```

Most of this is self explanatory, but check out the comments in the code to learn a bit more context. This isn't a prisma course, so we're going to keep moving along on our API. The rest of the modeling looks very much like this.

## User

```prisma
model User {
  id        String    @id @default(uuid())
  createdAt DateTime  @default(now())
  username  String    @unique
  password  String
  updates     Update[]
}
```

Above is our User schema

## Product

```prisma
model Product {
  id          String   @id @default(uuid())
  createdAt   DateTime @default(now())
  name        String
  belongsTo   User     @relation(fields: [belongsToId], references: [id])
  belongsToId String
  updates     Update[]
}
```

Here we have a Product schema. For the change log app, the user might have many products they want to update. So we need a place to store multiple updates. So `products` belong to a `User`.

## Update

```prisma
enum UPDATE_STATUS {
  IN_PROGRESS
  LIVE
  DEPRECATED
  ARCHIVED
}

model Update {
  id        String   @id @default(uuid())
  createdAt DateTime @default(now())
  updatedAt DateTime

  title   String        @db.VarChar(255)
  body    String
  status  UPDATE_STATUS @default(IN_PROGRESS)
  version String?
  asset   String

  productId    String
  product      Product       @relation(fields: [productId], references: [id])
  updatePoints UpdatePoint[]
}
```

Products can have updates. So products belong to updates. Updates have many fields, one is called status. Because status is a finite set of options, we created an ENUM to represent our status. Think of an enum value types as "one-of-these". So the value must be one of the values in the ENUM instead of being any other random string.

## Update Points

```prisma
model UpdatePoint {
  id        String   @id @default(uuid())
  createdAt DateTime @default(now())
  updatedAt DateTime

  name        String @db.VarChar(255)
  description String

  updateId String
  update   Update @relation(fields: [updateId], references: [id])
}
```

And finally, update points are the bullets points on an update. They belong to an update, which belongs to a product, which belongs to a user.

<br>
As we continue to build, we will most likely make changes to our schema to fit the experience we want to create.
