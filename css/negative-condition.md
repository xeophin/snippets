---
created: 2025-10-26T15:38
updated: 2025-11-01'T'09:36
title: Negative Condition
language: css
tags: webdev
---

```css
.some-element:not(.parent .some-element) {
 /* ... */
}
```

## What it does
This selects all items `.some-element` which are _not_ within the `.parent`.

## Why it's useful
This has been useful recently to handle cases where styles would only have to apply in _some_ versions of a website, but not others.

In our case it was easier to formulate that as a negative condition – as in: only do that if you're _not_ on the new version of the website.
This way, it was not necessary to define separate conditions for all the old versions.
Instead, we could update the CSS styles to how they should work in the new versions (and, how eventually they will work everywhere once the transition phase is complete), and add a fallback value for the old version, which we can then remove at some point.

It took me surprisingly long to find this solution – I was constantly trying to solve it using `:root:not(:has(.parent)) .some-element`, which incurs a heavy performance penalty.
I assume I came up with this first solution because it seemed more natural; going from a top selector drilling down to a bottom selector.

Instead it seems better to understand the `:not()` pseudo-class as a refinement selector of the element the rule is applied to.