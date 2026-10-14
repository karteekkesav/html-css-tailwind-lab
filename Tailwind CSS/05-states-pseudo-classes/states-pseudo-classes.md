# Tailwind States And Pseudo-classes

## What It Means

Tailwind uses variants to apply styles in specific states.

```text
hover:
focus:
active:
disabled:
checked:
group-hover:
```

## Button State Example

```html
<button class="bg-blue-600 hover:bg-blue-700 focus:ring-2 disabled:bg-slate-300">
  Save
</button>
```

Breakdown:

```text
bg-blue-600       = normal background
hover:bg-blue-700 = background on hover
focus:ring-2      = focus ring when keyboard/click focused
disabled:bg-*     = disabled button background
```

## Visual Diagram

```text
normal   -> blue
hover    -> darker blue
focus    -> visible ring
disabled -> gray
```

## Realtime Use Cases

- buttons
- links
- form inputs
- tab items
- dropdown menu items
- cards with hover feedback

## Interview Answer

Tailwind variants like `hover:`, `focus:`, and `disabled:` let me style UI states directly in markup. This is useful for interactive and accessible components.
