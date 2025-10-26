---
created: 2025-10-26T15:38
updated: 2025-10-26T20:43
title: Dividing by Units in CSS
requirements:
  - 
language: css
tags:
sources:
  - https://typetura.com/blog/unit-division-with-css-and-fallbacks/
---

```css
* {  
  /* Division magic */  
  --div: calc(var(--num) / var(--denom));  
}  
  
@supports not (width: calc(1% / 1px * 1px)) {  
  @property --num {  
   syntax: '<length>';  
   initial-value: 0px;  
   inherits: false;  
  }  
  @property --denom {  
   syntax: '<length>';  
   initial-value: 0px;  
   inherits: false;  
  }  
  * {  
   --NUM: calc(tan(atan2(var(--num), 1px)));  
   --DENOM: calc(tan(atan2(var(--denom), 1px)));  
   --div: calc(var(--NUM) / var(--DENOM));  
  }  
}   
  
.your-element {  
  --num: 100vw;  
  --denom: 1px;  
  --rotate: calc(var(--div) * 1deg);
}
```

## What it does

Currently, only Safari supports dividing one unit by another unit. This workaround gets it done for other browsers, too.


## Why it's useful

This allows you to normalise values and then use this normalised value to set other values with units.