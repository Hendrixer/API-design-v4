---
title: "What Prisma"
description: "What is Prisma and why do we need it"
---

## You need an ORM

When it comes to choosing a DB for your API, there are many variables at play. For the most part, you'll end up with a Relational (SQL) DB or a NoSql DB (Document Store). We're not going to get into what is the "best" DB because that's impossible to answer and changes as your product's needs change.

However, no matter the DB, how you interact with the DB matters. What good is the perfect DB that is painfull to interact with. Enter, and ORM. Object-Relational Mapper (ORM) is a term used to describe a technique that allows you to interact with a DB using an object-oriented approach. When most people say ORM, they're actually talking about an ORM library, which is really just and SDK for your DB. For example, without and ORM, you can only interact with a SQL DB using SQL.

```sql
INSERT INTO Customers (
  CustomerName,
  ContactName,
  Address,
  City,
  PostalCode,
  Country
)
  VALUES
  ('Cardinal',
  'Tom B. Erichsen',
  'Skagen 21',
  'Stavanger',
  '4006',
  'Norway'
  );
```

<br>
Using an ORM, depending on which one, your DB interaction for the same logic might look like this.

```javascript
db.customers.create({
  customerName: 'Cardinal',
  contactName: 'Tom B. Erichsen',
  address: 'Skagen 21',
  ....
})
```

You tell me: What looks easier to work with?
<br>
<br>
**Exactly.**
<br>
<br>

## What is Prisma

Prisma is a DB agnostic, type safe ORM. It supports most DBs out there. It not only has an SDK for doing basic and advanced querying of a DB, but also handles schemas, migrations, seeding, and sophisticated writes. It's slowly but surely becoming the ORM of choice for Node.js projects.
