# Tailwind Customization And Config Concepts

## What It Means

In real projects, Tailwind is usually customized through a config file.

Example concept:

```js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          600: "#2563eb"
        }
      }
    }
  }
};
```

Then you can use:

```html
<button class="bg-brand-600">Save</button>
```

## Why This Helps

```text
custom colors       = match product brand
spacing tokens      = consistent layouts
font family tokens  = match design system
breakpoints         = match application needs
```

## Interview Perspective

Tailwind is strongest when it follows a design system. Instead of random arbitrary values everywhere, teams define reusable tokens for color, spacing, typography, and breakpoints.

## Arbitrary Values

Tailwind allows arbitrary values:

```html
<div class="w-[420px] bg-[#2563eb]">
  Custom value
</div>
```

Use them carefully.

Interview answer: I use arbitrary values only when the value is truly unique. If it appears repeatedly, I move it into the Tailwind config or a shared component pattern.
