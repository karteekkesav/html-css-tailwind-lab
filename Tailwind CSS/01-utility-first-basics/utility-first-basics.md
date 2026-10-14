# Tailwind Utility-first Basics

## What It Means

Tailwind CSS is utility-first. That means we style elements using small classes that each represent one CSS rule or one small group of related rules.

Example:

```html
<button class="rounded bg-blue-600 px-4 py-2 text-white">
  Save
</button>
```

Breakdown:

```text
rounded      = border-radius
bg-blue-600  = background color
px-4         = left and right padding
py-2         = top and bottom padding
text-white   = text color
```

## Visual Diagram

```text
Traditional CSS
HTML class name -> custom CSS file -> styles

Tailwind
HTML utility classes -> styles directly visible in markup
```

## Plain CSS vs Tailwind

Plain CSS:

```html
<button class="primary-button">Save</button>
```

```css
.primary-button {
  padding: 8px 16px;
  border-radius: 6px;
  background: #2563eb;
  color: white;
}
```

Tailwind:

```html
<button class="rounded-md bg-blue-600 px-4 py-2 text-white">
  Save
</button>
```

Both create a styled button. Tailwind keeps the styling decision close to the markup.

## Realtime Use Case

In React applications, Tailwind is useful for:

- dashboard cards
- button components
- forms
- table rows
- responsive layouts
- onboarding pages
- admin panels

## Interview Answer

Tailwind is a utility-first CSS framework. Instead of writing custom CSS for every component, I compose UI using small utility classes like `p-4`, `flex`, `text-sm`, `bg-blue-600`, and `rounded-md`. This helps build consistent interfaces quickly, especially in component-based React applications.
