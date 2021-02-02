---
title: Utility Without the Clutter - Types Without TypeScript
author: Nico Rehwaldt
---

# _Utility Without the Clutter_

### Types Without TypeScript

---

#### A Talk by [`@nikku`](https://github.com/nikku)

---

## Why Types

* Safety during development
* Guards against dependencies
* Editor tooling / advanced assistance
* Easier consumption for your users :arrow_up:

---

## `tsc`, the [TypeScript](https://www.typescriptlang.org/) tool

* Checks your code base
* Transpiles your TypeScript to JavaScript
* Generates types from your JavaScript

---

## Why not Compile?

* <mark>Need to</mark> write `code.ts`
* <mark>Everything has to be transpiled</mark>
* <mark>Source maps</mark> bloat packages and are hard to debug

---

## Maintainer Wishlist

* My code base is checked
* My code base is typed (for consumers)

---

## Project Setup

```plain
.
├── src
│   ├── index.js
│   └── other.js
├── package.json
├── rollup.config.js
└── tsconfig.json
```

---

## TypeScript Configuration

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "allowJs": true,
    "checkJs": true,
    "strict": false,
    "skipLibCheck": true,
    ...
  },
  ...
}
```

---

## Add Type Definitions via JSDoc

```javascript
/**
 * @constructor
 * @param { { sayHello: boolean } } options
 */
export function Foo(options) {
  ...
}
```

<small>Cf. [TypeScript documentation](https://www.typescriptlang.org/docs/handbook/jsdoc-supported-types.html).</small>

---

## Or Import Type Definitions

```javascript

/**
 * @typedef { import('./types').FooOptions } FooOptions
 */

/**
 * @constructor
 * @param { FooOptions } options
 */
export function Foo(options) {
  ...
}
```

---

## Check Your Code Base

```plain
tsc --noEmit --pretty
```
<small>Cf. [TypeScript documentation](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html).</small>

---

## Generate Type Definitions

```plain
tsc src/index.js \
  --declaration \
  --emitDeclarationOnly \
  --removeComments \
  --outDir dist/types
```

<small>Cf. [TypeScript documentation](https://www.typescriptlang.org/docs/handbook/declaration-files/dts-from-js.html).</small>

---

## Expose Type Definitions

```json
{
  "name": "my-project",
  "main": "dist/index.js",
  "types": "dist/types/index.d.ts",
  ...
}
```

---

## Profit

```javascript
import {
  Foo
} from 'my-project';

const foo = new Foo({});
                    ^---- Argument of type '{}' is not assignable to
                          parameter of type '{ sayHello: boolean }'.
```

---

## :arrow_right: Types are developed and checked naturally, during development.

---

## Summary

* Haz types without `.ts` :cake: :medal:
* `tsc` tooling helps you out :muscle:

---

## Resources

* [TypeScript Documentation](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html) - On JS projects utilizing TypeScript
* [Skaat](https://github.com/nikku/skaat), [Wuffle](https://github.com/nikku/wuffle), [merge-me](https://github.com/nikku/merge-me) - Projects that follow the <em>types without TypeScript</em> approach

---

## Thanks

:clap: