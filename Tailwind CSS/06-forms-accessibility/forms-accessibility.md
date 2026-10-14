# Tailwind Forms, Focus States, And Accessibility

## What It Means

Tailwind can style forms quickly, but accessibility still depends on correct HTML and visible states.

## Accessible Input Example

```html
<label for="email">Email</label>
<input id="email" class="focus:ring-2 focus:ring-blue-500">
```

The label is connected to the input with `for` and `id`.

## Focus State

```html
<input class="border px-3 py-2 focus:border-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-200">
```

```text
focus:border-blue-600 = border changes on focus
focus:ring-2          = visible focus ring
```

## Error State

```html
<input class="border-red-500 ring-2 ring-red-100">
<p class="text-sm text-red-600">Email is required</p>
```

## Interview Answer

For forms, I use semantic labels, clear error messages, visible focus rings, readable spacing, and sufficient color contrast. Tailwind makes the styling fast, but accessibility comes from both HTML structure and CSS states.
