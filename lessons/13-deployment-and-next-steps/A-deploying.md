We now need to deploy our API so we can use it! We just need to consider a few things. There really aren't too many things we need to change right now to make sure we can deploy. It also depends on where you're deploying.

<br>
For us, the most imporant thing is making sure our repo is on Github and we create a build script to build our TypeScript.
<br>
In our package.json:

```json
"scripts": {
  "build": "tsc -p tsconfig.json",
  "start": "node dist/index.js",
}
```

Render.com will use these scripts to build and start our server. Last thing is one final adjustment to our tsconfig.

```json
{
  "compilerOptions": {
    "sourceMap": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": false,
    "lib": ["esnext"],
    "esModuleInterop": true,
    "declaration": true
  },
  "include": ["src/**/*.ts"]
}
```

We're ready to deploy!
