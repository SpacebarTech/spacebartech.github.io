---
layout: default
title: Publishing NPM Packages
category: process
permalink: "/process/publishing-npm-packages"
---

# {{ page.title }}

## Scoped packages

All packages published under the JETS Technologies name are
to be published as `scoped`. To publish a scoped package,
log into NPM with `npm login` with the credentials
available on Dashlane.

```sh
npm login --registry=http://registry.npmjs.org --scope=@jetstech
```

Once logged in, create your new project and run `npm init
-y`. Make sure to set the project name in the `package.json`
to `@jetstech/some-project`.

Once you've gotten the project to a usable state, you can
publish it with the following:

```sh
npm publish --access restricted # for private packages
npm publish --access public     # for publicly available packages
```

You can then install your newly created project using:

```sh
npm i @jetstech/some-project
```

## Updating the version

If you've made some additions to the project and want to
push a new release to NPM, you can increment the version
number in the `package.json`, and then simply run the
following (without the `--access` flags):

```sh
npm publish
```
