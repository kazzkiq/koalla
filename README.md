<p align="center">
  <img width="834" alt="koalla" src="https://user-images.githubusercontent.com/1953194/235337240-2bafcfcf-05a3-4b3d-9524-2d762cf74d50.png">
  <br><br><br>
  <b>Koalla CLI 🐨</b>
  <br>
   A CLI for minimalist back-end projects.
</p>
<br><br>

## What is Koalla?

Koalla is a simple and lean project scaffolding for building Node.js Web APIs.

It aims to be a sane middleground between the dozen scattered options of super-opinionated back-end frameworks such as Nest.js and Adonis, and the super-loose "figure everything by yourself" standalone frameworks like Koa.js and Express.js.

There is nothing wrong with either super-opinionated or super-loose frameworks, but they're not for everybody.

If you like to have a sane base to build up your API, that gives you the basics to get going while also keeping all your freedom to change whatever you like, then Koalla may be a good fit for you.

## Features
- 🌿 Performance: Uses [Koa](https://koajs.com/) as web framework & router.
- 🌿 Tests: Uses [uvu](https://github.com/lukeed/uvu) for blazing fast™  unit & endpoints testing.
- 🌿 Safety: TypeScript by default.
- 🌿 Flexibility: No enforced patterns other than routes filenames.
- 🌿 Comfort: Live-reload out of the box.
- 🌿 Productivity: A minimal CLI that generates endpoints for you.
- 🌿 Docs: Add some comments to your routes and get Swagger docs.


## Getting started
To get started with Koalla, simply run:

```
npx koalla init my-project
```

And that's it! You now have the base for your new back-end ready to go with all the above features in less than 10 seconds!

## Creating routes

To create a new route you can use the `new route` command:


```
npx koalla new route products
```

This command will generate two files for you:
- `src/endpoints/products.ts`
- `src/routes/products.ts`

### Endpoints
Endpoints are where you'll put your endpoints logic. A typical file looks like this:

```ts
import { RouterContext } from "@koa/router";
import Koa from "koa";

export const ExampleEndpoints = {
  async read(ctx: Koa.Context & RouterContext, next: Koa.Next) {
    ctx.status = 200;
    ctx.body = {
      message: "Hello!",
    };
    next();
  },
};
```

This is the pattern Koalla and the CLI uses, but you're free write those files as you please. As long as your function (or class method) receives Koa's `ctx` and `next` and keep compliance, everything else is allowed.

### Routes
Routes are where you'll find the path that runs your endpoints. A typical file looks like this:

```ts
import Koa from "koa";
import Router, { RouterContext } from "@koa/router";

import { ExampleEndpoints } from "@/endpoints/example";

const router = new Router();

router.get("/", ApiStatusEndpoints.read);

export default router.routes();
```

Alternatively, you can enable swagger docs by adding a few comments:


```ts
import Koa from "koa";
import Router, { RouterContext } from "@koa/router";

import { ExampleEndpoints } from "@/endpoints/example";

const router = new Router();

router.get(
  "/",
  async (ctx: Koa.BaseContext & RouterContext, next: Koa.Next) => {
    /*
    #swagger.tags = ['Example']
    #swagger.responses[200] = {
      schema: {
        message: "Hello.",
      }
    }
    */

    return ExampleEndpoints.read.call(this, ctx, next);
  }
);

export default router.routes();
```

Koalla uses [swagger-autogen](https://github.com/davibaltar/swagger-autogen), visit the docs for further instructions on all the available comments.

## Special Thanks

Koalla can be described simply as a smart backpack with cool tools inside it organized and ready for you to use.

This means Koalla wouldn't be possible without the great efforts of those tools:
- [Koa.js](https://koajs.com/)
- [uvu](https://github.com/lukeed/uvu)
- [sade](https://github.com/lukeed/sade)
- [swagger-autogen](https://github.com/davibaltar/swagger-autogen)
- and [much others](https://github.com/kazzkiq/koalla-skeleton/blob/main/package.json#L33).
