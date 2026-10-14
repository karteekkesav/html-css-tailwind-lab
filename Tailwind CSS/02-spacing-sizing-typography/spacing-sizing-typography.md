# Tailwind Spacing, Sizing, Colors, And Typography

## What It Means

Tailwind provides utility classes for common design values.

```text
p-4       padding
m-4       margin
w-full    width: 100%
max-w-xl  max-width
text-sm   font size
font-bold font weight
bg-*      background color
text-*    text color
```

## Spacing Example

```html
<div class="p-6 m-4">
  Card content
</div>
```

```text
p-6 = padding inside the card
m-4 = margin outside the card
```

Visual:

```text
margin outside
  +----------------------+
  | padding inside       |
  | Card content         |
  +----------------------+
```

## Directional Spacing

```text
p-4  = padding all sides
px-4 = padding left and right
py-2 = padding top and bottom
pt-4 = padding top
mb-6 = margin bottom
```

Button example:

```html
<button class="px-4 py-2">Save</button>
```

## Sizing Example

```html
<div class="w-full max-w-md">
  Form container
</div>
```

```text
w-full   = take full available width
max-w-md = do not grow beyond medium max width
```

## Typography Example

```html
<h1 class="text-3xl font-bold text-slate-900">
  Dashboard
</h1>
```

## Interview Answer

Tailwind spacing and sizing utilities make layout consistent. I use `p`, `m`, `px`, `py`, `gap`, and `space-y` for spacing, `w-full` and `max-w-*` for responsive sizing, and typography utilities like `text-sm`, `text-xl`, and `font-semibold` for readable UI.
