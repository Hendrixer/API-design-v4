---
title: "Tools"
description: "What tools we will be using for this course"
---

# Tools

When it comes to building out production ready API's, there are several moving pieces and for each one, there are several options to choose from. We won't be covering EVERY single detail in this course, instead we'll cover the common tools that you'll need.

## Runtime

We'll be using **Node.js** for this course. Why? Node.js uses JS as it's language of choice. If you've worked on web apps, then you know JS. Node.js has a rich, active ecosystem as well. I also know Node.js the best. Alternatives include (Ruby, Python, Java, Go, Rust, many many more).

## Framework

We could create an API without a framework, but that wouldn't be the best use of our time and isn't taking advantage of an amazing ecosystem at our fingertips. So, we'll be using **Express** to create our API inside of Node.js

## Database

There are so many great options these days when it comes to choosing a database. For the most part. We'll be using **Psql** or _Postgres_. It's one of the most popular DB's in the world and gives of tons of options when its time to deploy our API. For the ORM, we'll be using Prisma to interact with our DB. Primsa has proven itself a very valuable tool that we can leverage to create schemas, query our DB, and even handle migrations. It also works for several databases.

## Hosting

When it comes to hosting an Node.js based API, you can pretty much close your eyes then point in any direction and you'll be sure to land on a platform that supports node. This is not a DevOps class, so we want to use a platform that manages it all for us. For that, we'll be using **Render**.
