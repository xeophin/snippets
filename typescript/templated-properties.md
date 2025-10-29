---
created: 2025-10-29T11:29
updated: 2025-10-29T12:10
title: Templated Properties
requirements:
  - typescript
language: typescript
tags:
  - datawrangling
  - webdev
sources:
  - 
---

```typescript

interface GenericProperties {
	productName: string
	price: number
	store: string
}

enum Country {
	CH = 'ch',
	DE = 'de',
}

export type ProductProperties = {
	[Property in keyof GenericProperties as `${Property}_${Country}`]: GenericProperties[Property];
}
```

This will produce an object of the form

```typescript
const products: ProductProperties = {
	productName_ch: 'Blevita',
	price_ch: 15.2,
	store_ch: 'Migros'
	productName_de: 'Dar-Vida',
	price_de: 12.48,
	store_de: 'Rewe'
}
```

Given the templated form, constructs like this will then also be fine:

```typescript

function getProductName(country: Country) {
	return products[`productName_${country}`]
}

```


## What it does

Using a combination of interfaces and enums as well as template strings allows you to quickly define complex types without having to repeat yourself too often.


## Why it's useful

Data journalists often provide you with a CSV with a lot of columns. In the best case, the column names are not entirely random, but have repeating patterns that group common properties.

While typing these files using AI is certainly possible (because AI will happily write you tons of tedious, repetitive code), using this templating approach might be more flexible and extensible.
In fact, it might even be worth it to quickly transform the data file using [Nushell](convert-csv-to-tsv.md) or similar tools