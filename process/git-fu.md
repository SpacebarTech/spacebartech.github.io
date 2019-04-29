---
layout: default
title: Git-Fu
category: process
permalink: "/process/git-fu"
---

# {{ page.title }}

## Have limited experience with Git?

- Talk to your fellow teammates and let them know where you
  stand
- Read the documentation, and don't be too intimidated. Git
  has many commands that allow the user to precisely
  specify what needs to happen. However, you can get by
  very well with just a couple of commands.

## Custom `git` commands

### A better `git log`

`git log` is useful, but it displays commits in a very
verbose way and does not illustrate the git graph very well.
The solution is to add [a better git log](https://coderwall.com/p/euwpig/a-better-git-log)
command. Follow the instructions at the link to set up the
command.

### List recently committed-to branches

When jumping around branches (e.g. when QA'ing someone
else's feature), you can sometimes forget what branch you
were previously working on.

To list branches that you have committed to recently
(oldest to most recent), try this out:

```bash
git branch --sort=-committerdate | tac
```

Now as a `git` alias:

```bash
git config --global alias.recent "! git branch --sort=committerdate | tac"
```

If you added the alias, use it like this: `git recent`. The
branches that you are probably interested in will be at the
bottom.

### Delete local branches with no remotes

Often times, when branches are merged from a pull request,
local branches tend to stay behind and not get removed.
It can cause your `git checkout` from being simple to being
staggering, making branches hard to find. And while VSCode
is user-friendly in that it shows latest branches near the
top, that won't always be the case.

To clean up those unneeded branches, run the following:

```bash
git fetch -p && for branch in `git branch -vv | grep ': gone]' | awk '{print $1}'`; do git branch -D $branch; done
```

## Changing your default editor for Git

Select the application you would like to open for commit
messages and completing a merge or rebase.

### Vim

```bash
git config --global core.editor "vim"
```

### VSCode

```bash
git config --global core.editor "code --wait"
```

### VSCode Insiders

```bash
git config --global core.editor "code-insiders --wait"
```

## Commit messages

At JETS, we use Commitizen for our commit messages. You can
access `cz-cli` by opening up your favorite Terminal and
running the following command, and following through the
prompts:

```bash
git-cz
```

Typically, commitizen is installed via a global npm install,
but err on the side of doing local installs for almost all
other packages and project dependencies.

Take a look at [how to write a git commit message](https://chris.beams.io/posts/git-commit/)
by Chris Beams. The seven rules he mentions are good rules
of thumb. The most important ones are keeping the subject
(the main message of the commit) short, and also "Using the
imperative mood in the subject line" (e.g. doing the action
in the present). This can be something like the following:

- "Fix xyz"
- "Correct xyz"
- "Close #xxxx"
- "Remove xyz"
- etc.

**This is so important.**
