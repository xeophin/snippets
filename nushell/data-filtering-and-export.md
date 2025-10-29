---
created: 2025-03-11T09:03
updated: 2025-10-29T11:10
title: Extracting Information from a CSV using nushell
requirements:
  - nushell
language:
  - nushell
tags: datawrangling
---

```nushell
open mongodb_export.users.csv | where role == 'teacher' | select name email dateCreated dateLastLogin | save teacher-accounts.csv
```

## What it does
Takes a CSV, filters it based on a predicate (`where`), chooses specific columns (`select`) and exports the whole thing in a new CSV.


## Why it's useful
Offers a quick way to clean up a CSV file that would otherwise not be up for consumption.