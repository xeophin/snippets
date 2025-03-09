---
title: Setting up a Git repository using worktrees
created: 2025-03-09T17:08
updated: 2025-03-09T17:48
requirements:
  - git
language: shell
tags: 
sources:
  - https://morgan.cugerone.com/blog/workarounds-to-git-worktree-using-bare-repository-and-cannot-fetch-remote-branches/
  - https://morgan.cugerone.com/blog/how-to-use-git-worktree-and-in-a-clean-way/
---

Cloning a bare repository. This does not contain any files; instead it puts the files that are usually in a hidden `.git` folder directly in the top level.

```sh
git clone --bare git@github.com:myname:my-awesome-project.git
```

However, this does not retain the information that is needed to fetch from the remote. This can be added using

```sh
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"
```

Add a new worktree:

```sh
git worktree add name-of-the-feature
```

This will add a new directory with the specific branch checked out. 

## Why is it useful?

This allows you to have different directories with different branches checked out. No more switching between branches anymore.