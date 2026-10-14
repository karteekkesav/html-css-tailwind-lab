# Forms, Focus, And Accessibility

## What It Means

CSS should support accessible form interaction through visible focus, readable error states, and clear disabled states.

## Diagram

```text
default -> hover -> focus -> error -> disabled
```

## Resume-Based Example

For POI, POA, and liveness verification workflows, users must clearly see which field is active and which fields need correction.

## Interview Answer

I keep focus indicators visible, use high-contrast error states, avoid relying on color alone, and style disabled fields so they remain understandable.

## Common Mistakes

- Removing outlines without replacement.
- Showing errors only with red color.
- Making disabled controls unreadable.
