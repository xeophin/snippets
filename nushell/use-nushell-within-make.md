---
created: 2025-10-29T11:10
updated: 2025-10-29T11:10
title: Use Nushell in a Makefile
requirements:
  - nushell
  - make
language: nushell
tags: datawrangling
---

```make
output.tsv: input.csv  
  nu -c "open $< | to tsv | save $@ -f"
```

## What it does
Runs a Nushell one-liner as part of a makefile. Reads the input file (`$<`), transforms it, and writes it to the target file `$@`.

## Why it's useful
Nushell contains various tools to manipulate tabular data with a fairly nice syntax, making it a good tool to quickly transform some data from some format to another.