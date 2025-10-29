---
created: 2025-03-11T09:03
updated: 2025-10-29T11:10
title: Export
requirements:
  - nushell
language:
  - nushell
tags: datawrangling
---

```nushell
open list.json | each {|e| save $"($e.title).json"}
```

## What it does

Given a JSON file of the form

```jsonc
[
	{
		"title": "Something",
		// additional properties …
	},
	{
		"title": "Else",
		// additional properties …
	},
	{
		"title": "Another",
		// additional properties …
	},
]
```

The snippet will take the list and split it apart into single files, each named after the title property.

## Why it's useful
Quick way to split apart a JSON array into individual files. Easily adaptable to other file formats (think CSV).