# z-index And Stacking Context

## What It Means

`z-index` controls the stacking order of positioned elements, but it works inside stacking contexts.

## Diagram

```text
page stacking context
|
+-- modal layer z-index: 1000
+-- header layer z-index: 100
+-- card layer z-index: 1
```

## Basic z-index Example

`z-index` controls which element appears in front when elements overlap.

Example:

```html
<div class="box red">Red</div>
<div class="box blue">Blue</div>
```

```css
.box {
  position: absolute;
  width: 120px;
  height: 120px;
}

.red {
  background: red;
  left: 40px;
  top: 40px;
  z-index: 1;
}

.blue {
  background: blue;
  left: 80px;
  top: 80px;
  z-index: 2;
}
```

Visual:

```text
Red and blue overlap.
Blue appears on top because z-index: 2 is greater than z-index: 1.
```

```text
higher z-index = appears in front
lower z-index  = appears behind
```

Important: `z-index` works most predictably on positioned elements, such as:

```css
position: relative;
position: absolute;
position: fixed;
position: sticky;
```

## Realtime Example: Badge On Card

```html
<div class="card">
  <img src="profile.jpg" alt="Profile">
  <span class="badge">New</span>
</div>
```

```css
.card {
  position: relative;
  width: 300px;
}

.card img {
  width: 100%;
}

.badge {
  position: absolute;
  top: 12px;
  right: 12px;
  z-index: 2;
  background: #2563eb;
  color: white;
  padding: 4px 8px;
}
```

Visual:

```text
+------------------------------+
| image                  [New] |
|                              |
|                              |
+------------------------------+
```

Explanation:

```text
.card position: relative = badge is positioned inside the card
.badge position: absolute = badge is placed at top/right
.badge z-index: 2 = badge appears above the image
```

## Realtime Example: Modal Above Page

```html
<header class="header">Header</header>
<main class="page">Page Content</main>
<div class="modal">Modal</div>
```

```css
.header {
  position: sticky;
  top: 0;
  z-index: 100;
}

.modal {
  position: fixed;
  inset: 0;
  z-index: 1000;
}
```

Visual:

```text
z-index: 1000  modal
z-index: 100   header
z-index: auto  page content
```

The modal appears above the header because `1000` is higher than `100`.

## Why z-index Sometimes Does Not Work

`z-index` works inside stacking contexts. A child cannot always escape its parent's stacking context just by using a very large value.

Example:

```html
<div class="card">
  <div class="tooltip">Tooltip</div>
</div>

<div class="modal">Modal</div>
```

```css
.card {
  position: relative;
  z-index: 1;
}

.tooltip {
  position: absolute;
  z-index: 9999;
}

.modal {
  position: fixed;
  z-index: 100;
}
```

Even though `.tooltip` has `z-index: 9999`, it may still appear below `.modal` because it is inside `.card`, and `.card` is only at `z-index: 1`.

Visual:

```text
page stacking context
|
+-- modal z-index: 100
+-- card  z-index: 1
    |
    +-- tooltip z-index: 9999 inside card only
```

Interview explanation: When `z-index` seems broken, I check whether a parent created a stacking context.

## Stacking Context Triggers

- Positioned element with `z-index`
- `opacity` less than 1
- `transform`
- `filter`
- `isolation: isolate`

## Resume-Based Example

In enterprise apps, z-index matters for modals, dropdowns, tooltips, sticky headers, and document upload overlays.

## Interview Answer

If z-index is not working, I inspect parent stacking contexts. A child cannot escape its parent's stacking context just by increasing z-index.
