---
created: 2026-04-17T14:03
updated: 2026-04-17T14:04
title: Pull an External Repo into an Existing Repo
requirements:
  - git
language:
  - shell
tags:
sources:
  - https://www.atlassian.com/git/tutorials/git-subtree
---
```shell
# Within an existing repo
git subtree add --prefix directory/to/place/external-repo git@github.com:user/external-repo.git main
```
## What it does
Pulls an external repo into an existing repo, and places it in the directory set with `--prefix`.
Retains the history (unless you use the `--squash` switch).

## Why it's useful
Useful for creating a monorepo out of already existing packages.
This way you can make sure that the history remains and isn't thrown away when migrating to the monorepo.
Apparently it's also possible to update the subtree using `git subtree pull`.
This makes it a good candidate for pulling in code (i.e. plugins) into your dotfiles.