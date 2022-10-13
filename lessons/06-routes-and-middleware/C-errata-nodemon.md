---
title: "Errata - Nodemon Setup"
description: "Auto-restart the server with Nodemon"
---

## Nodemon

Throughout the course, Scott is manually stopping and starting the server anytime changes in the source code occurs. This was an intential decision to reduce the complexity of the setup. However, if you want your server to auto-restart when there is a change, you can use [nodemon](https://nodemon.io/).

### Nodemon Setup Instructions

Install nodemon

```bash
npm install nodemon --save-dev
```

> nodemon is a installed as a development dependency because, once the application is deployed, the web host will be responsible for starting the server.

Once nodemon is installed, update the `dev` script in your package.json file

```json
"dev": "nodemon src/index.ts"
```
