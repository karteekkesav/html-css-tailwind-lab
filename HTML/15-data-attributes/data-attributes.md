# data Attributes

## What It Means

`data-*` attributes store custom data directly on HTML elements.

Example: `data-user-id="42"`.

## Interview Answer

Data attributes are useful for storing small, non-sensitive metadata in HTML. They can support testing, analytics, progressive enhancement, or JavaScript behavior. I avoid using them for sensitive data or large application state.

## Common Mistakes

- Storing private information in HTML.
- Using data attributes instead of proper state management for complex apps.
- Overusing them when semantic attributes already exist.

## Quick Revision

Use `data-*` for small custom metadata.
