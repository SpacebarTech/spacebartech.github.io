---
layout: default
title: Create a TypeScript Library
category: engineering
permalink: "/engineering/create-typescript-library"
---

# {{ page.title }}

## Using the starter kit

## Building from scratch

Building a TypeScript library from scratch means the user
has better control over the flow of the library itself:
the Github repository, scoped packages, and other
architectural decisions. While there is benefit to using
the [Starter Kit](), there is absolutely nothing wrong with
a Library built from scratch. There are, however, a few key
differences between the two.

1. You won't be able to perform automatic publishing
   through a CI unless you add the necessary scripts
   yourself.
2. Barrels aren't automatically generated.
3. There's no `genfn` bin script. All files must be made
   manually.
4. There are no pre-commit handlers
5. Automatic documentation generation
6. Several others...

There are plenty of examples on how to structure a library.
All libraries will be structured identically.

### Add a function

When adding a new function, follow the pattern:

```perl
src/
  {fileName}/
    {fileName}.ts
    {fileName}.spec.ts
```

Note that all filenames are `camelCased`. When adding a new
function, you don't have to worry about generating barrels.
You only need to worry about this when prepping for a new
release.

If you have `helper` functions that you don't want to be
published, then the folder structure will look like so:

```perl
src/
  helpers/
    ...
  lib/
    {fileName}/
      {fileName}.ts
      {fileName}.spec.ts
```

### Building

Before publishing, you must also build the project. In the
past, this happened in the `postinstall` script, but it
required that the end-user had TypeScript installed on
their system. This is really, really annoying. Build it
before publishing.

```sh
npm run build
```

### Barrels

The automatic generation of `barrel`s is a key feature of
the [Starter Kit](). This allows each function within `src/`
to become available as exported modules. Before publishing
a new release, you must run the following, otherwise some
functions may be unavailable.

```sh
npm run generate-barrels
```

This script re-exports nested modules to the top-level
`index.ts`

### Deployments

Since you won't be able to do automatic deployments to NPM
once CI passes, you'll have to add these scripts yourself.
If this isn't a priority, simply `npm login` to the
`@jetstech` NPM scope, and run `npm publish` manually. Be
sure to increment the version number in the `package.json`!
Keep in mind that a Library should be a real-world
open-source library. When publishing, use the `--access
public` flag, like so:

```sh
npm publish --access public
```

If for whatever reason a library should be restricted,
publish with `--access restricted` instead.
