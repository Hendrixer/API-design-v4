---
title: "API Anatomy"
---

## Little bits

Every API ever shares a common make up. Doesn't matter the language or the environment. What makes them different is how each one does it and what they build on top if. Let's talk about all those common bits that make up an API.

## Server

An API is a **Server**. This may seem obvious, but really needs to be understood. A server is an app that has no visual representation and is always running. Usually connected to a network and shared among many clients (UIs, web apps, mobile apps, other servers, etc). Servers usually sit in front of a DB and facilitate access to that DB. There are small exceptions here, and that would be Serverless APIs. Big difference with serverless APIs is they are not always on like a traditional server. Servers must operate on a port, a virtual place on a computers operating system where network connections start and end. Ports help computers sort out their network traffic. A server must also have an IP address, a unique location used to locate a server on a network, like the internet. An IP address helps traffic go to and from a specific device whereas a port allows targeting of specific services or apps on a device. An example would look like this:
`127.0.0.1:5000`. Where `5000` is the port and the rest is the IP address.

## Route

A route is a unique combination of a URL path and a HTTP Method. Routes are used to locate certain resources or trigger certain actions on an API.

HTTP Methods or Verbs are constants that are used by API developers and HTTP to help determine intent of an API call. There are many methods, but the common ones are:

- `GET` - used to get information from an API
- `POST` - used to mutate or create new information on an API. Usually has data sent along with the request.
- `PUT` - used to replace existing information on an API. Usually has data sent along with the request.
- `PATCH` - used to update existing information on an API. Usually has data sent along with the request.
- `DELETE`- used to remove existing information on an API.
- `OPTIONS` - used with CORS by browsers to check to see if the client is able to actually communicate with an API

Here are some examples of routes:

- `GET /api/user/1`
- `POST /food`

Engineers can design these routes and what the routes actually do however they see fit. To standardize this, there are different approaches to designing these routes. The most popular is REST. There are others like grpc, graphql, and protobuff.

## Route Handlers

A route handler is a function that executes when a certain route is triggered from an incoming request. Depending on the API design and intent of the request, the handler will interact with the database. Looking at our route examples above:

- `GET /api/user/1` - if this API was a REST API, the route handler would query the database for a user with the ID of 1.

- `POST /food` - if this API was a REST API, the route handler would create a new food in the database, using the data sent along with the request.
