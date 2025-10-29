---
created: 2025-05-23T17:53
updated: 2025-10-29T12:10
title: DOM Manipulation
language:
  - javascript
  - svelte
  - typescript
requirements:
  - svelte@>=5.29
---
```svelte
<script lang="ts">  
   import type { Attachment } from "svelte/attachments";  
  
   const pullSubsequentParagraphIn: Attachment<HTMLDivElement> = (container: HTMLDivElement) => {  
   // Find containing article component  
   const containingArticleComponent = container.closest('.articlecomponent.q-embed')  
  
   if (containingArticleComponent === undefined) return  
  
   // Select next article component  
   const nextParagraph = containingArticleComponent!.nextElementSibling  
  
   if (nextParagraph === null || !nextParagraph.matches('p.articlecomponent')) return  
  
   container.appendChild(nextParagraph)  
  }  
</script>  
  
<div {@attach pullSubsequentParagraphIn}></div>

```

## What it does
Uses the new [Attachements](https://svelte.dev/docs/svelte/@attach) from svelte. But could certainly also work in a [use:](https://svelte.dev/docs/svelte/use) property.

It takes the element in question and traverses the DOM tree from there.

`element.closest()` climbs the tree **up**, and selects the containing element that matches the selector – so we can figure out the container in which our component has been mounted in.

`element.nextElementSibling` gives back the next sibling element.

`element.matches()` can be used to check that the element in question matches a specific selector.

`element.appendChild()` moves a node at another place in the DOM tree.

## Why is it useful
In cases where you want to manipulate the DOM directly – useful for us at NZZ Editorial Tech when we want to integrate other content that's on an article page into our components.
