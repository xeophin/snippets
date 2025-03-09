---
title: Using `git sparse-checkout` to limit to focus on a directory
created: 2025-03-09T17:08
updated: 2025-03-09T17:48
requirements:
  - git
language: shell
tags: 
sources:
  - https://git-scm.com/docs/git-sparse-checkout
---

```sh
git sparse-checkout set <directory-to-focus>
```

```sh
git sparse-checkout add <additional-directory>
```


## Why is it useful?

A sparse checkout allows you to limit the amount of files that are being checked out in your worktree. In a multi-project repository, this might be nice, as it lessens the workload of your IDE, that doesn't have to index all the files that you are not going to use anyway.