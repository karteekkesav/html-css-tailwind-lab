# CSS Variables And Theming

## What It Means

CSS variables store reusable values and support design tokens and themes.

## Diagram

```text
:root tokens
|
+-- button
+-- card
+-- form
+-- dashboard
```

## Example

```css
:root {
  --color-primary: #0f766e;
  --space-md: 16px;
}
```

## Resume-Based Example

CSS variables map well to Figma tokens, Tailwind themes, and MUI design systems.

## Interview Answer

I use CSS variables for consistent colors, spacing, typography, and theme switching. They make large React applications easier to maintain.
