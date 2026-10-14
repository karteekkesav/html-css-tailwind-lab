# ARIA Attributes

## What It Means

ARIA means Accessible Rich Internet Applications. ARIA attributes add accessibility information to elements when native HTML cannot fully describe a custom UI.

## Useful ARIA Attributes

- `aria-label`
- `aria-labelledby`
- `aria-describedby`
- `aria-expanded`
- `aria-controls`
- `aria-live`

## Interview Answer

ARIA helps assistive technologies understand custom components, but I prefer native HTML first. For example, I use a real `button` before adding `role="button"` to a `div`. Incorrect ARIA can make accessibility worse.

## Common Mistakes

- Adding ARIA where native HTML already works.
- Using `role="button"` without keyboard support.
- Setting `aria-expanded` but not updating its value.

## Quick Revision

First rule of ARIA: prefer native HTML.
