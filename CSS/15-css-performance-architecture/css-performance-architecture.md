# CSS Performance And Architecture

## What It Means

CSS performance is about efficient rendering. CSS architecture is about organizing styles so large projects remain maintainable.

## Diagram

```text
Design tokens
|
+-- base styles
+-- layout utilities
+-- components
+-- page-specific styles
```

## Performance Tips

- Remove unused CSS.
- Keep selectors simple.
- Avoid large layout shifts.
- Animate `transform` and `opacity`.
- Use responsive images and stable dimensions.
- Avoid unnecessary DOM depth.

## Architecture Tips

- Use reusable component styles.
- Use design tokens or CSS variables.
- Keep global styles limited.
- Use consistent naming.
- Align with Tailwind, MUI, or CSS Modules when used by the project.

## Resume-Based Example

For React enterprise apps, style architecture matters because onboarding modules, shared libraries, and dashboard components must remain consistent across teams and releases.

## Interview Answer

I optimize CSS by reducing unused styles, keeping selectors simple, avoiding expensive animations, and organizing styles around tokens and reusable components.
