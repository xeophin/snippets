---
created: 2026-07-17T08:25
updated: 2026-07-17T08:25
title: Lazy Initialisation
requirements:
  - typescript
language: typescript
tags:
  - webdev
sources:
  - 
---

```typescript
import { Helmlab, type Hex } from 'helmlab';
import { formatHex, parse } from 'culori';

let hl: Helmlab | undefined;

function getHelmlab(): Helmlab {
	return (hl ??= new Helmlab());
}

function normalizeHex(color: Hex): Hex {
	const parsed = parse(color);
	return ((parsed && formatHex(parsed)) ?? color) as Hex;
}

/**
 * Uses the Helmlab color model to create a similar colour for the dark mode from a color that has been optimised
 * for the light mode.
 * @param color
 */
export function createDarkModeColorFromLightModeColor(color: Hex) {
	return getHelmlab().ensureContrast(normalizeHex(color), '#000000', 5);
}

export function createLightModeColorFromDarkModeColor(color: Hex) {
	return getHelmlab().ensureContrast(normalizeHex(color), '#FFFFFF', 5);
}
```


## What it does

The module keeps a single, module-scoped `hl` variable that starts out `undefined`. Instead of constructing the `Helmlab` instance at import time, `getHelmlab()` only creates it the first time it's actually needed, using the nullish-coalescing assignment operator `??=`. On every call, `hl ??= new Helmlab()` checks whether `hl` is `null` or `undefined`; if so, it assigns the right-hand side and evaluates to that value, otherwise it just returns the existing instance. Every exported function then calls `getHelmlab()` instead of referencing `hl` directly, so callers never need to worry about whether the instance already exists.

## Why it's useful

Some objects are expensive or undesirable to construct eagerly, for example because they load data, open a connection, or simply aren't needed on every code path. Lazy initialisation defers that cost until the first real use, and the `??=` operator makes the "create once, reuse afterwards" logic a single expression instead of a manual `if (hl === undefined)` check. It also naturally gives you a module-level singleton without extra classes or dependency-injection machinery, which is handy for small, stateless helper libraries like a color model that don't need more than one instance per process.
