---
layout: default
title: NPM vs. Yarn
category: engineering
permalink: /engineering/npm-v-yarn
---

# {{ page.title }}

Once upon a time, [Yarn](https://yarnpkg.com/en/) was
lightyears ahead of NPM in terms of speed and efficiency.
Where `npm rebuild` might fail, `yarn` might've taken a
different approach and succeed. It's weird quirks like this
that caused Yarn to take the stage to begin with.
Specifically with React apps, `yarn` tended to be the
preferred package manager.

In 2019, though, NPM has caught up in both speed and
efficiency. While Yarn is only slightly faster now, NPM
seems to have gotten a lot of bugs fleshed out and is very
stable to use. That's why JETS has stuck with NPM. The very
marginal speed boost is simply not enough to warrant the
installation of yet another package manager.

Now, all of our docs reflec the use of NPM instead of Yarn,
although Yarn can still be used.

More documentation around this with stats will come later
in the future so that it turns from an unbiased entry to
one of fact.
