---
created: 2026-04-17T13:43
updated: 2026-04-17T14:04
title: List JSON Properties from Sub-Directories
requirements:
  - nushell
language:
  - nushell
tags:
sources:
  - 
---
```nushell
ls */package.json | each {|pkg| open $pkg.name | select name version }
```

## What it does
Goes through all the `package.json` files in the subdirectories, and for each of those files extracts the name and the version.

## Why it's useful
When the data in several subdirectories, and you want to turn them into one list or table.