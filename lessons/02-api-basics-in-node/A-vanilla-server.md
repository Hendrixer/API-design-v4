---
title: "Vanilla API"
description: "Build a vanilla, no framework used, API in node.js"
---

## Playing on hard mode

Node.js comes with everything you need to build a fully functional API. However, it's very tedious and unwise to use the raw modules. For context and appreciation of frameworks, let's do it anyway!

```javascript
import http from "http";

const server = http.createServer(async (req, res) => {
  if (req.url === "/" && req.method === "GET") {
    res.writeHead(200, { "Content-Type": "application/json" });
    res.write(JSON.stringify({ message: "hello" }));

    res.end();
    return;
  }

  res.writeHead(404, { "Content-Type": "application/json" });
  res.end(JSON.stringify({ message: "nope" }));
});

const PORT = process.env.PORT;

server.listen(PORT, () => {
  console.log(`server on ${PORT}`);
});
```

... and just like that, we have an API. It doesn't do much functionally, but it works. A client can issue a `GET` request to the server at `/` and get back some JSON. Any other request will yield a different message and a `404` status code. We'll talk about HTTP Methods, status codes, and routes later in the course.

## Why this breaks down

When building something trivial like our example, then not using a framework is fine. Maybe even preferred. But you'll have to start creating your abstractions as soon as you build anything. Why create your own when a framework is just that: Abstractions based on some opinions that benefit from having community support.
