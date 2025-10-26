---
created: 2025-03-09T17:57
updated: 2025-10-26T15:38
title: Some nice title
requirements:
  - svelte@>=5
language: svelte
tags: webdev
---

```svelte
<script>
let isBroken = $state(false)
</script>

<img
	src={imgSrc}
	onerror={() => (isBroken = true)}
	class:isBroken
/>

<style>
.isBroken {
	display: none;
}
</style>
```

## What it does
When a request for an image source fails (i.e. there has been a 404), the state of the component is set to `broken`; it which point the image element is hidden.


## Why it's useful
In cases where the image src is constructed from other parameters and a successful retrieval is not guaranteed, you might want to hide the element entirely, instead of being left with a sad broken image icon.