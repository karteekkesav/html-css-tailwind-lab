# Tailwind Flexbox And Grid Layouts

## What It Means

Tailwind provides utilities for Flexbox and Grid.

```text
flex              display: flex
items-center      align-items: center
justify-between   justify-content: space-between
grid              display: grid
grid-cols-3       three columns
gap-4             gap between items
```

## Flexbox Example

```html
<div class="flex items-center justify-between gap-4">
  <h2>Users</h2>
  <button>Add User</button>
</div>
```

Visual:

```text
+--------------------------------+
| Users                [Add User]|
+--------------------------------+
```

Use Flexbox for one-dimensional alignment:

```text
navbars
toolbars
button groups
card headers
centered content
```

## Grid Example

```html
<section class="grid grid-cols-3 gap-4">
  <div>Users</div>
  <div>Revenue</div>
  <div>Orders</div>
</section>
```

Visual:

```text
+----------+ +----------+ +----------+
| Users    | | Revenue  | | Orders   |
+----------+ +----------+ +----------+
```

Use Grid for two-dimensional layouts:

```text
dashboards
card grids
page shells
content/sidebar layouts
galleries
```

## Interview Answer

I use Tailwind Flexbox utilities for one-dimensional alignment and Grid utilities for rows and columns. For example, `flex items-center justify-between` is great for a card header, while `grid grid-cols-3 gap-4` is better for dashboard cards.
