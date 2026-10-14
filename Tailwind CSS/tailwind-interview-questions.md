# Tailwind CSS Interview Questions Quick Review

Use this file for fast revision before interviews.

## 1. What Is Tailwind CSS?

Tailwind CSS is a utility-first CSS framework. Instead of writing custom CSS classes for every component, we compose UI using small utility classes directly in HTML or JSX.

Example:

```html
<button class="rounded bg-blue-600 px-4 py-2 text-white">
  Save
</button>
```

Interview answer: Tailwind helps build consistent UI quickly using reusable utility classes for spacing, color, typography, layout, and states.

## 2. What Does Utility-first Mean?

Utility-first means each class usually does one small styling job.

```html
<div class="p-4 border rounded">
  Card content
</div>
```

```text
p-4     = padding
border  = border
rounded = border radius
```

Interview answer: Utility-first CSS reduces context switching because I can see most styling directly where the markup is written.

## 3. Tailwind vs Plain CSS?

```text
Plain CSS = write custom class names and CSS rules
Tailwind  = compose UI with existing utility classes
```

Plain CSS:

```css
.primary-button {
  padding: 8px 16px;
  background: #2563eb;
  color: white;
}
```

Tailwind:

```html
<button class="bg-blue-600 px-4 py-2 text-white">
  Save
</button>
```

Interview answer: Plain CSS gives full control and separation. Tailwind gives speed, consistency, and fewer custom CSS files.

## 4. How Do Responsive Classes Work?

Tailwind is mobile-first. Unprefixed classes apply to all screen sizes. Prefixed classes apply from that breakpoint and above.

```html
<div class="grid grid-cols-1 gap-4 md:grid-cols-3">
  ...
</div>
```

```text
grid-cols-1    = mobile/default one column
md:grid-cols-3 = 3 columns from md breakpoint and above
```

Interview answer: `md:` does not mean mobile. It means apply from the `md` breakpoint and larger.

## 5. How Do Hover And Focus Work?

Tailwind uses variants like `hover:` and `focus:`.

```html
<button class="bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500">
  Save
</button>
```

Interview answer: Variants apply utilities only in a specific state, such as hover, focus, active, disabled, or dark mode.

## 6. How Do You Build Layouts In Tailwind?

Use Grid for page-level layouts and Flexbox for component alignment.

```html
<main class="grid grid-cols-1 gap-6 lg:grid-cols-[240px_1fr]">
  <aside>Sidebar</aside>
  <section>Content</section>
</main>
```

```html
<div class="flex items-center justify-between gap-4">
  <h2>Users</h2>
  <button>Add</button>
</div>
```

Interview answer: I use Grid for two-dimensional page layouts and Flexbox for one-dimensional alignment inside components.

## 7. How Do You Handle Forms And Accessibility?

Use readable labels, visible focus states, disabled states, and sufficient color contrast.

```html
<input class="w-full rounded border px-3 py-2 focus:border-blue-600 focus:ring-2 focus:ring-blue-200">
```

Interview answer: Tailwind makes accessible states easy because focus rings, disabled styles, and error styles can be added directly with utility classes.

## 8. What Is `space-y-*`?

`space-y-*` adds vertical spacing between direct children.

```html
<div class="space-y-4">
  <p>One</p>
  <p>Two</p>
  <p>Three</p>
</div>
```

Interview answer: I use `space-y-*` for stacked content and `gap-*` for Flexbox/Grid layouts.

## 9. What Is The Difference Between `p-4`, `px-4`, And `py-4`?

```text
p-4  = padding on all sides
px-4 = left and right padding
py-4 = top and bottom padding
```

Example:

```html
<button class="px-4 py-2">Save</button>
```

## 10. How Do You Reuse Components?

In React, reusable components keep Tailwind classes in one place.

```jsx
function Button({ children }) {
  return (
    <button className="rounded bg-blue-600 px-4 py-2 text-white hover:bg-blue-700">
      {children}
    </button>
  );
}
```

Interview answer: I avoid repeating long class strings everywhere by creating reusable components, shared variants, or helper utilities when needed.

## 11. How Does Tailwind Help Performance?

In production, Tailwind scans project files and generates only the classes that are used.

Interview answer: Tailwind can produce small production CSS because unused utilities are removed during the build process.

## 12. What Are Common Tailwind Mistakes?

- Using too many arbitrary values without a design system.
- Repeating long class strings instead of creating components.
- Forgetting mobile-first behavior.
- Removing focus styles without replacing them.
- Using responsive prefixes incorrectly.

## Final Cheat Sheet

```text
Utility-first: small classes composed in markup
Responsive: default mobile, md/lg and above with prefixes
Spacing: p, m, px, py, gap, space-y
Layout: flex for one axis, grid for rows and columns
States: hover, focus, active, disabled
Accessibility: labels, contrast, focus rings
Reuse: React components, variants, class helpers
Performance: production build removes unused CSS
```
