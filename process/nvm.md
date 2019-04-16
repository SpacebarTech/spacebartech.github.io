---
layout: default
title: nvm
category: process
permalink: "/process/nvm"
---

# {{ page.title }}

Instead of installing a specific version of NodeJS to your
system, it is recommended that you use a Node version
manager to manage development needs.

If you use bash shell, use [nvm](https://github.com/creationix/nvm).
If you use the Fish shell, use the [fisherman](https://github.com/fisherman/fisherman)
to install [fnm](https://github.com/fisherman/fnm) for your
node versioning needs.

## `.nvmrc`

You can see the output of a project's `.nvmrc` file by
running the following:

```bash
cat .nvmrc
```

This file is used to indicate the version of Node being
used in a project. Run the commands `nvm use` or `fnm use`
to sync up your Node version with that of the project
directory.

## Call `nvm use` automatically

If you use bash shell, add the following after your NVM
initialization in `$HOME/.bashrc` to automatically call
`nvm use` when you `cd` into a directory:

```bash
find-up () {
  path=$(pwd)
  while [[ "$path" != "" && ! -e "$path/$1" ]]; do
    path=${path%/*}
  done
  echo "$path"
}

cdnvm(){
  cd "$@";
  nvm_path=$(find-up .nvmrc | tr -d '[:space:]')

  # If there are no .nvmrc file, use the default nvm version
  if [[ ! $nvm_path = *[^[:space:]]* ]]; then

    declare default_version;
    default_version=$(nvm version default);

    # If there is no default version, set it to `node`
    # This will use the latest version on your machine
    if [[ $default_version == "N/A" ]]; then
      nvm alias default node;
      default_version=$(nvm version default);
    fi

    # If the current version is not the default version, set it to use thdefault version
    if [[ $(nvm current) != "$default_version" ]]; then
      nvm use default;
    fi

    elif [[ -s $nvm_path/.nvmrc && -r $nvm_path/.nvmrc ]]; then
    declare nvm_version
    nvm_version=$(<"$nvm_path"/.nvmrc)

    declare locally_resolved_nvm_version
    # `nvm ls` will check all locally-available versions
    # If there are multiple matching versions, take the latest one
    # Remove the `->` and `*` characters and spaces
    # `locally_resolved_nvm_version` will be `N/A` if no local versions are found
    locally_resolved_nvm_version=$(nvm ls --no-colors $(<"./.nvmrc") | tail -1 | tr -d '\->*' | tr -d '[:space:]')

    # If it is not already installed, install it
    # `nvm install` will implicitly use the newly-installed version
    if [[ "$locally_resolved_nvm_version" == "N/A" ]]; then
      nvm install "$nvm_version";
    elif [[ $(nvm current) != "$locally_resolved_nvm_version" ]]; then
      nvm use "$nvm_version";
    fi
  fi
}
alias cd='cdnvm'
```

If you use [zsh](https://www.zsh.org/), add the following
to your `$HOME/.zshrc`:

```zsh
# place this after nvm initialization!
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

## Updating Node version

To update Node, update the `.nvmrc` with the respective
project. Continuous integration and Docker will pull this
version when building. Don't use different Node versions
between your local project and Docker, or CI.
