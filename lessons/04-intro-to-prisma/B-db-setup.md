---
title: "DB Setup"
description: "Setup our DB and install Prisma"
---

## Psql

We'll be using PSQL as a DB in this course. You won't have to install anything as we'll be using a hosting and managed DB from [Render](https://render.com). Go there, create an account, and then create a FREE psql DB.

## Installing Prisma

Prisma works best when you're using a TypeScript. So in addition to installing Prisma, we're going to convert our app to TypeScript. Don't worry if you don't know TypeScript. We won't be doing all the fancy typed stuff in this course. We just want that sweet autocomplete for our DB interactions through Prisma. Trust me, its magical ✨. On to the installing!
<br>
<br>
`npm i typescript ts-node @types/node prisma --save-dev`
<br>
<br>
Then create a `tsconfig.json` file which is the config file for TypeScript. Add this to that file:
<br>

```json
{
  "compilerOptions": {
    "sourceMap": true,
    "outDir": "dist",
    "strict": true,
    "lib": ["esnext"],
    "esModuleInterop": true
  }
}
```

<br>
<br>
Next, we'll initalize Prisma
<br>

`npx prisma init`

<br>
This command will do a few things:

- Create a prisma folder
- Create a schema file in that folder
  Next, we'll learn how to design and create some models in our schema
