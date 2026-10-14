# CSS Units

## What It Means

CSS units define size, spacing, width, height, typography, and layout measurements.

Common units:

```text
px   fixed
%    relative to parent
em   relative to current element font size
rem  relative to root font size
vw   viewport width
vh   viewport height
fr   grid fraction
```

## 1. px Fixed Unit

`px` means pixels. It is a fixed size.

```css
.box {
  width: 300px;
  padding: 20px;
}
```

Meaning:

```text
width   = exactly 300px
padding = exactly 20px
```

Visual:

```text
+------------------------------+
| fixed 300px box              |
+------------------------------+
```

Realtime uses:

```text
borders
small icons
fixed sidebar width
precise small spacing
```

Interview answer: `px` is a fixed unit. It does not depend on the parent, font size, or viewport.

## 2. % Relative To Parent

`%` is relative to the parent or containing block.

```html
<div class="parent">
  <div class="child">Child</div>
</div>
```

```css
.parent {
  width: 800px;
}

.child {
  width: 50%;
}
```

Calculation:

```text
child width = 50% of parent width
child width = 50% of 800px
child width = 400px
```

Visual:

```text
Parent: 800px
+----------------------------------------+
| Child: 400px                           |
+--------------------+                   |
```

Realtime uses:

```text
fluid containers
responsive widths
image sizing
layout sections
```

Interview answer: `%` is useful when an element should scale based on its parent size.

## 3. em Relative To Current Element Font Size

`em` is relative to the current element's computed font size.

Example:

```css
.button {
  font-size: 16px;
  padding: 1em;
}
```

Calculation:

```text
button font-size = 16px
1em              = 16px
padding          = 16px
```

If the font size changes:

```css
.button {
  font-size: 20px;
  padding: 1em;
}
```

Now:

```text
button font-size = 20px
1em              = 20px
padding          = 20px
```

## If A Button Has Multiple em Properties

All `em` values use the same current element font size.

```css
.button {
  font-size: 20px;
  padding: 1em;
  margin: 2em;
  border-radius: 0.5em;
}
```

Calculation:

```text
font-size = 20px
padding: 1em        = 20px
margin: 2em         = 40px
border-radius: .5em = 10px
```

Important: `em` does not check all properties. It uses the element's computed `font-size`.

## If Child Has No font-size

If the child does not define `font-size`, it inherits font size from its parent.

```html
<div class="parent">
  <button class="button">Save</button>
</div>
```

```css
.parent {
  font-size: 18px;
}

.button {
  padding: 1em;
}
```

Calculation:

```text
parent font-size = 18px
button font-size = inherited 18px
padding: 1em     = 18px
```

## If Parent And Child Both Have No font-size

If neither the parent nor the child defines `font-size`, the element uses the inherited browser/root default.

Usually:

```text
browser default font-size = 16px
```

Example:

```html
<div class="parent">
  <button class="button">Save</button>
</div>
```

```css
.parent {
  /* no font-size */
}

.button {
  padding: 1em;
}
```

Calculation:

```text
html/browser font-size = usually 16px
parent font-size       = inherited 16px
button font-size       = inherited 16px
padding: 1em           = 16px
```

Inheritance flow:

```text
browser default/html font-size
        ↓
parent element
        ↓
child element
```

Interview answer: `em` is calculated from the current element's computed font size. If the element has no font size, it inherits from the parent. If no parent defines it either, it usually falls back to the browser default, commonly `16px`.

## 4. rem Relative To Root Font Size

`rem` is relative to the root `<html>` font size.

```css
html {
  font-size: 16px;
}

.card {
  padding: 2rem;
}
```

Calculation:

```text
1rem = 16px
2rem = 32px
```

Unlike `em`, `rem` does not depend on the current element's font size.

Example:

```css
html {
  font-size: 16px;
}

.parent {
  font-size: 20px;
}

.child {
  padding: 2rem;
}
```

Calculation:

```text
2rem = 2 * root font-size
2rem = 2 * 16px
2rem = 32px
```

The parent's `20px` font size does not affect `rem`.

Realtime uses:

```text
consistent spacing
font sizes
design systems
responsive typography
```

Interview answer: I prefer `rem` for consistent spacing and typography because it is based on the root font size.

## em vs rem

```text
em  = relative to current element font size
rem = relative to root/html font size
```

Example:

```css
html {
  font-size: 16px;
}

.button {
  font-size: 20px;
  padding: 1em;
  margin-bottom: 1rem;
}
```

Calculation:

```text
padding: 1em       = 20px because button font-size is 20px
margin-bottom: 1rem = 16px because root font-size is 16px
```

## 5. vw Viewport Width

`vw` means viewport width.

```css
.hero {
  width: 100vw;
}
```

Meaning:

```text
100vw = 100% of browser viewport width
50vw  = 50% of browser viewport width
```

If viewport width is `1200px`:

```text
50vw = 600px
```

Visual:

```text
Viewport width: 1200px
+------------------------------------------------+
| 100vw element fills full viewport width         |
+------------------------------------------------+
```

Realtime uses:

```text
full-width sections
hero layouts
viewport-based sizing
```

Interview answer: `vw` is useful when a size should depend on the browser width.

## 6. vh Viewport Height

`vh` means viewport height.

```css
.hero {
  min-height: 100vh;
}
```

Meaning:

```text
100vh = full visible browser height
```

If viewport height is `800px`:

```text
100vh = 800px
```

Visual:

```text
Viewport height
+----------------------+
|                      |
|  100vh section       |
|                      |
+----------------------+
```

Realtime uses:

```text
full-screen hero section
login page
app shell
centered page layout
```

Interview answer: `vh` is useful when a section should be based on the browser height, such as `min-height: 100vh` for full-screen layouts.

## 7. fr Grid Fraction Unit

`fr` is used in CSS Grid. It divides available space into fractions.

```css
.layout {
  display: grid;
  grid-template-columns: 1fr 2fr;
}
```

Meaning:

```text
total parts = 1 + 2 = 3
first column = 1 part
second column = 2 parts
```

Visual:

```text
+-------------+--------------------------+
| 1fr         | 2fr                      |
+-------------+--------------------------+
```

Example:

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

Meaning:

```text
3 equal columns
```

Visual:

```text
+----------+ +----------+ +----------+
| 1fr      | | 1fr      | | 1fr      |
+----------+ +----------+ +----------+
```

Important: `fr` divides the remaining space after fixed sizes and gaps are considered.

```css
.dashboard {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: 16px;
}
```

Meaning:

```text
first column = fixed 240px
gap          = 16px
second column = remaining space
```

Interview answer: `fr` is useful in CSS Grid when columns or rows should share available space.

## Quick Interview Answer

```text
px  = fixed size
%   = relative to parent
em  = relative to current element font size
rem = relative to root font size
vw  = relative to viewport width
vh  = relative to viewport height
fr  = fraction of available space in CSS Grid
```

## Resume-Based Example

Use `rem` for scalable spacing and typography, `%` for fluid containers, and `fr` for dashboard grid columns.

## Interview Answer

I choose units based on the layout need. I use `rem` for consistent spacing, `%` for fluid widths, `fr` for Grid layouts, `px` for precise small values like borders, and viewport units carefully for full-screen sections.
