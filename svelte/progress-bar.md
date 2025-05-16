---
created: 2025-05-16T14:15
updated: 2025-05-16T14:15
title: Svelte Scroll Progress Bar
requirements:
  - svelte@>=5
language: svelte
tags: webdev
---

```svelte
<script lang="ts">  
  import { innerHeight } from 'svelte/reactivity/window'  
  
  interface Props {  
   container: HTMLElement  
  }  
  
  const { container }: Props = $props()  
  let containerTop = $state(0)  
  let elementHeight = $derived(container?.clientHeight)  
  let baseHeight = $derived(elementHeight - innerHeight.current)  
  let scrollDistance = $derived(-1 * containerTop)  
  let completion = $derived(  
   Math.max(0, Math.min(scrollDistance / baseHeight, 1)),  
  )  
  
  const onscroll = () => {  
   containerTop = container?.getBoundingClientRect().top  
  }  
</script>  
  
<svelte:window {onscroll} />  
<div>  
  <div style:width={`${completion * 100}%`}></div>  
</div>  
  
<style>  
  div {  
   height: 3px;  
   background-color: var(--articleBackground, #ffffff);
   position: sticky;
   top: 0;
   width: 100%  
  
   > div {  
    display: block;  
    background-color: var(--accent-color);  
    transition: width 50ms ease-in-out;  
    height: 3px;  
   }  
  }  
</style>
```

## What it does
This component takes a HTML element and produces a progress bar, that shows how much of that element has already been scrolled through.


## Why it's useful
Mostly useful for scrolly elements, where we want to give an indication how long the scroll element is going to take to scroll through.