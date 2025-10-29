---
created: 2025-10-26T15:38
updated: 2025-10-29T12:10
title: Popovers with Fallback
requirements:
  - 
language:
  - javascript
  - svelte
  - typescript
tags:
sources:
  - 
---

```svelte
<script lang="ts">    
  import InfoIcon from '@nzz-private/nzz-icons/optimized/24/information.svg';   
  import { createDashIdent, createId } from '@src/utils/dashIdent';  
  
  // A list of objects
  const buttons = [
	  {
		  name: 'Foo',
		  description: 'This is a foo button.'
	  },
	  {
		  name: 'Bar',
		  description: 'This is a bar button.'
	  }
  ]

// check if the browser supports anchor positioning
  const supportsAnchorPositioning = CSS.supports('position-anchor', '--anchor-id');  
  
  const showPopover = (event: MouseEvent | FocusEvent) => {  
   const button = event.currentTarget as HTMLButtonElement;   
   if (supportsAnchorPositioning) {
    button.popoverTargetElement?.showPopover({source: button});  
   } else {  
    button.popoverTargetElement?.classList.add('open');  
   }  
  };  
  
  const hidePopover = (event: MouseEvent | FocusEvent) => {  
   const button = event.currentTarget as HTMLButtonElement;   
   if (supportsAnchorPositioning) {  
    button.popoverTargetElement?.hidePopover();  
   } else {  
    button.popoverTargetElement?.classList.remove('open');  
   }  
  };  
</script>  
  
<fieldset> 
  <div class="buttons">  
   {#each buttons as {name}}  
    <button 
     popovertarget={createId(cartInfo.displayName)}  
     onmouseenter={showPopover}  
     onmouseleave={hidePopover}  
     onfocus={showPopover}  
     onblur={hidePopover}  
     >{name}  
    </button> 
   {/each}  
  </div>  
  
  <div class="infobox">  
   <img src={InfoIcon} alt="information" />  
   {#each buttons as {name, description}, index}  
    <div   
     popover="hint"  
     style:--anchor-id={createDashIdent(name)}  
     id={createId(name)}  
    >  
     {description}  
    </div>  
   {/each}  
  </div>  
</fieldset>  
  
<style>  
  
  @supports not (position-anchor: --anchor-id) {  
   .infobox {  
    display: flex;  
    margin-block: 1rlh;  
    gap: 1ch;  
    align-items: baseline;  
  
    &:has(:global([popover].open)) img {  
     display: block;  
    }  
  
    img {  
     display: none;  
     height: 1lh;  
     width: auto;  
     align-self: start;  
    }  
   }  
  
   [popover] {  
    margin: 0;  
    border: none;  
    padding: 0;  
    max-width: revert;  
    width: 100%;  
    height: auto;  
    position: static;  
    background: none;  
    overflow: revert;  
    inset: unset;  
  
    :global(&.open) {  
     display: block;  
    }  
   }  
  }  
  
  @supports (position-anchor: --anchor-id) {  
   .infobox {  
    img {  
     display: none;  
    }  
   }  
  
   [popover] {  
    position: absolute;  
    margin: 1ex;  
    inset: auto;  
    position-anchor: var(--anchor-id);  
    top: anchor(bottom);  
    justify-self: anchor-center;  
    position-try: normal flip-block;  
   }  
  }  
</style>
```

## What it does

Uses the HTML popover feature to show tooltips for buttons. The tooltips are placed using anchor-positioning.

If the browser does not support anchor positioning, place the tooltips below the buttons and show them when hovering over the button.

An alternative would be to place the tooltips with JavaScript using the mouse position or the measurements of the buttons – but why do it with JavaScript if you could use a fancy CSS feature instead?

## Usage Notes

- `showPopover()` will set the element to `display: block;` and move it into the [top layer](https://developer.mozilla.org/en-US/docs/Glossary/Top_layer), effectively taking the element out of the document flow.
  
  If anchor positioning is not available, I want the element to stay within the document flow; hence the workaround with the `open` class which only toggles the `display` property.

- Setting the `popover` attribute on an element will add some default styling from the user agent – this has to be overriden (e.g. padding, borders, background color, margins, position)

## Why it's useful

Even with anchor positioning support missing, the content of the tooltips is displayed.