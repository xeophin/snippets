---
created: 2025-10-29T11:10
updated: 2025-10-29T11:10
title: Convert a CSV to a TSV file
requirements:
  - nushell
language: nushell
tags: datawrangling
---

```nushell
open table.csv --raw | from csv --separator ';'| rename --column { old_column_name: NewColumn, } | to tsv | save table.tsv -f
```

## What it does

Converts a CSV file to a TSV file. This specific snippet does the following things:
- Opens the file as a plain text file
- Reads it as a CSV – but with the separator `;` (which happens especially with Excel set to German)
- Renames specific columns to other names (useful in cases where the original columns contain whitespace in their names, which is less useful)
- Convert to TSV
- Save to a new file, overwriting already existing versions.