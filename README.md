# `@rowinbot/tsconfig`

> NOTE: This is currently just a clone of [@total-typescript/tsconfig](https://github.com/total-typescript/tsconfig) but the idea is to add more options and make it more opinionated and tailored to the projects I work on.

## Recognition

This package is very much inspired by the work of Matt Pocock on [`@total-typescript/tsconfig`](https://github.com/total-typescript/tsconfig). Without his work, this package would not exist. I highly recommend checking out his work and the [Total TypeScript](https://www.totaltypescript.com/) course.

## Setup

1. Install:

```bash
npm install --save-dev @rowinbot/tsconfig
```

2. Choose which `tsconfig.json` you need from the [list](#list-of-tsconfigs) below.

3. Add it to your `tsconfig.json`:

```jsonc
{
  // I'm building an app that runs in the DOM with an external bundler
  "extends": "@rowinbot/tsconfig/bundler/dom/app"
}
```

## List of TSConfigs

The tricky thing about `tsconfig.json` is there is _not_ a single config file that can work for everyone. But, with two or three questions, we can get there:

### Are You Using `tsc` To Turn Your `.ts` Files Into `.js` Files?

#### Yes

If yes, use this selection of configs:

```jsonc
{
  // My code runs in the DOM:
  "extends": "@rowinbot/tsconfig/tsc/dom/app", // For an app
  "extends": "@rowinbot/tsconfig/tsc/dom/library", // For a library
  "extends": "@rowinbot/tsconfig/tsc/dom/library-monorepo", // For a library in a monorepo

  // My code _doesn't_ run in the DOM (for instance, in Node.js):
  "extends": "@rowinbot/tsconfig/tsc/no-dom/app", // For an app
  "extends": "@rowinbot/tsconfig/tsc/no-dom/library", // For a library
  "extends": "@rowinbot/tsconfig/tsc/no-dom/library-monorepo" // For a library in a monorepo
}
```

#### No

If no, you're probably using an external bundler. Most frontend frameworks, like Vite, Remix, Astro, Nuxt, and others, will fall into this category. If so, use this selection of configs:

```jsonc
{
  // My code runs in the DOM:
  "extends": "@rowinbot/tsconfig/bundler/dom/app", // For an app
  "extends": "@rowinbot/tsconfig/bundler/dom/library", // For a library
  "extends": "@rowinbot/tsconfig/bundler/dom/library-monorepo", // For a library in a monorepo

  // My code _doesn't_ run in the DOM (for instance, in Node.js):
  "extends": "@rowinbot/tsconfig/bundler/no-dom/app", // For an app
  "extends": "@rowinbot/tsconfig/bundler/no-dom/library", // For a library
  "extends": "@rowinbot/tsconfig/bundler/no-dom/library-monorepo" // For a library in a monorepo
}
```

## Options Not Covered:

### `jsx`

If your app has JSX, you can set the `jsx` option in your `tsconfig.json`:

```json
{
  "extends": "@rowinbot/tsconfig/bundler/dom/app",
  "compilerOptions": {
    "jsx": "react-jsx"
  }
}
```

### `outDir`

Mostly relevant for when you're transpiling with `tsc`. If you want to change the output directory of your compiled files, you can set the `outDir` option in your `tsconfig.json`:

```json
{
  "extends": "@rowinbot/tsconfig/tsc/no-dom/library",
  "compilerOptions": {
    "outDir": "dist"
  }
}
```

### Framework-Specific Options

I don't yet cover framework-specific options, like `vite`, `next`, `remix`, etc. With enough persuasion, I might add them in the future.

## Why Not Use `@tsconfig/bases`?

The [`@tsconfig/bases`](https://github.com/tsconfig/bases) package is a great resource for TypeScript configurations. However, I disagree with the idea that there is a single "recommended" configuration that works for everyone.

Also, I wanted a set of `tsconfig.json` files that I controlled so I could use them to keep my [Total TypeScript Course Repos](https://github.com/rowinbot) up to date.

If you're looking for a great TypeScript course, check out [Total TypeScript](https://www.totaltypescript.com/).
