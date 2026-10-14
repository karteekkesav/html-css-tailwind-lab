# Tailwind Responsive Design

## What It Means

Tailwind is mobile-first.

Unprefixed classes apply to all screen sizes. Prefixed classes apply from that breakpoint and above.

```html
<div class="grid grid-cols-1 md:grid-cols-3">
  ...
</div>
```

```text
grid-cols-1    = mobile/default
md:grid-cols-3 = medium screens and above
```

## Visual Diagram

```text
Mobile:
+----------+
| Card 1   |
+----------+
| Card 2   |
+----------+

Desktop:
+----------+ +----------+ +----------+
| Card 1   | | Card 2   | | Card 3   |
+----------+ +----------+ +----------+
```

## Common Breakpoint Prefixes

```text
sm: small and above
md: medium and above
lg: large and above
xl: extra large and above
2xl: very large and above
```

Important interview point:

```text
md: does not mean mobile
md: means medium breakpoint and larger
```

## Example

```html
<section class="grid grid-cols-1 gap-4 md:grid-cols-2 lg:grid-cols-4">
  ...
</section>
```

```text
mobile  = 1 column
tablet  = 2 columns
desktop = 4 columns
```

## Interview Answer

Tailwind responsive classes are mobile-first. I write the default mobile layout first, then use prefixes like `md:` and `lg:` to enhance the layout for larger screens.
