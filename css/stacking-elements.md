---
created: 2025-10-26
updated: 2025-10-26T20:34
title: Stacking Elements in CSS
requirements:
  - 
language: css
tags: webdev
sources:
  - 
---

```css
.container {
	display: grid;
	grid-template-areas: 'content';
	
	& > * {
		grid-area: content;
	}
}
```

## What it does

Usually, block-level elements won't stack on top of each other.
Using a grid changes that.
I knew for some time that you can place blocks that overlap each other.
But this also means all the blocks may overlap each other – which means they are stacked on top of each other.

## Why it's useful

Before, stacking elements on top of each other meant using a container with `position: relative` and placing the other elements with `position: absolute`.
However, that would also mean that the contained elements would no longer contribute to sizing the container, so you have to set that manually.
By using the grid trick, the contained elements will still size the container correctly.

This trick is especially useful in combination with Svelte's transitions, in cases where one element is supposed to replace another.
By placing both (or more) elements in the grid container, it's possible to smoothly transition from one element to the other.