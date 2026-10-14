# Display And Positioning

## What It Means

`display` controls how an element participates in layout.

`position` controls how an element is placed on the page.

Simple interview difference:

```text
display  = how the element behaves in layout
position = where the element is placed
```

Example:

```css
.card {
  display: flex;
  position: relative;
}
```

Here:

```text
display: flex      = arrange children using Flexbox
position: relative = make this card a reference point for positioned children
```

## Display Diagram

```text
block        full row
inline       inside text flow
inline-block inline flow with box sizing
flex         one-dimensional layout
grid         two-dimensional layout
none         removed from layout
```

## Position Diagram

```text
static   normal flow
relative shifted from itself
absolute nearest positioned ancestor
fixed    viewport
sticky   scroll threshold
```

## display: block

A block element starts on a new line and takes the full available width of its parent by default.

Common block elements:

```text
div, p, section, article, header, footer, h1-h6
```

Example:

```html
<div class="card">Card One</div>
<div class="card">Card Two</div>
```

```css
.card {
  display: block;
  padding: 16px;
  border: 1px solid #d1d5db;
  margin-bottom: 12px;
}
```

Visual:

```text
+--------------------------------------+
| Card One                             |
+--------------------------------------+

+--------------------------------------+
| Card Two                             |
+--------------------------------------+
```

Interview explanation: I use block elements for sections, containers, cards, paragraphs, and layout rows because they naturally stack vertically.

## display: inline

An inline element stays inside the text flow and only takes as much width as its content.

Common inline elements:

```text
span, a, strong, em, label
```

Example:

```html
<p>
  Status:
  <span class="status-text">Approved</span>
</p>
```

```css
.status-text {
  display: inline;
  color: #15803d;
  font-weight: 700;
}
```

Visual:

```text
Status: Approved
```

Important: `width` and `height` do not work normally on inline elements.

```css
.status-text {
  width: 200px;
  height: 50px;
}
```

The above will not behave like a block box because the element is inline.

## Do width And height Work On Inline Elements?

For normal inline elements like `<span>` and `<a>`, explicit `width` and `height` do not apply in the normal box-layout way.

Example:

```html
<p>
  Status:
  <span class="status-text">Approved</span>
</p>
```

```css
.status-text {
  display: inline;
  width: 200px;
  height: 50px;
  background: #dcfce7;
}
```

Even though `width: 200px` and `height: 50px` are written, the span will still size mainly based on its text content.

Visual idea:

```text
Status: [Approved]
```

Not like this:

```text
Status: [Approved                         ]
```

So the answer is:

```text
width  = ignored for normal inline elements
height = ignored for normal inline elements
```

But some properties can still affect the visual space of inline elements.

### 1. Text Content Affects Width

```html
<span class="label">New</span>
<span class="label">Very Long Label Text</span>
```

The second span naturally takes more horizontal space because the text is longer.

```text
[New]
[Very Long Label Text]
```

Interview explanation: Inline elements size themselves based on their content, not a declared width.

### 2. font-size Affects Size

```css
.status-text {
  font-size: 24px;
}
```

Increasing `font-size` makes the inline text visually larger, so the inline box also appears larger.

### 3. line-height Affects Line Box Height

```css
.status-text {
  line-height: 40px;
}
```

`line-height` can affect the height of the line in which the inline element sits.

Important: this is not the same as setting `height: 40px`.

```text
height      = ignored on normal inline elements
line-height = affects the text line height
```

### 4. Horizontal Padding Works More Noticeably

```css
.status-text {
  padding-left: 12px;
  padding-right: 12px;
  background: #dcfce7;
}
```

This adds space on the left and right of the inline text.

Visual:

```text
Status: [   Approved   ]
```

### 5. Vertical Padding Can Look Tricky

```css
.status-text {
  padding-top: 12px;
  padding-bottom: 12px;
  background: #dcfce7;
}
```

Vertical padding may paint visually above and below the text, but it does not push surrounding lines the same predictable way a block or inline-block element does.

This is why badges and tags commonly use `inline-block`.

```css
.status-text {
  display: inline-block;
  padding: 8px 12px;
  width: 120px;
  height: 36px;
}
```

Now `width`, `height`, padding, and margin behave more like a regular box.

Best interview answer: For normal inline elements, `width` and `height` do not apply like they do on block elements. Inline elements size based on their content. If I need width, height, padding, or margin to behave predictably while keeping the element inline, I use `display: inline-block`.

Interview explanation: Inline elements are best for styling small pieces of text inside a sentence or line.

## display: inline-block

`inline-block` keeps the element in inline flow, but allows box-model properties like width, height, padding, and margin to work more predictably.

Example:

```html
<span class="tag">HTML</span>
<span class="tag">CSS</span>
<span class="tag">JavaScript</span>
```

```css
.tag {
  display: inline-block;
  padding: 6px 12px;
  margin: 4px;
  border: 1px solid #d1d5db;
}
```

Visual:

```text
[ HTML ] [ CSS ] [ JavaScript ]
```

Why `inline-block` helps:

```text
inline behavior = elements stay side by side
block behavior  = padding, width, height work properly
```

Realtime example: tags, badges, chips, pill buttons, small labels.

Interview explanation: I use `inline-block` when I want an element to sit inline but still behave like a box.

## display: flex

Flexbox is a one-dimensional layout system. It arranges items in a row or column.

Example: navbar

```html
<nav class="navbar">
  <a>Home</a>
  <a>About</a>
  <a>Contact</a>
</nav>
```

```css
.navbar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 24px;
}
```

Visual:

```text
Home      About      Contact
```

## justify-content vs align-items

Both `justify-content` and `align-items` are Flexbox alignment properties, but they work on different axes.

For default Flexbox:

```css
.navbar {
  display: flex;
  flex-direction: row;
}
```

The axes are:

```text
main axis  = horizontal
cross axis = vertical
```

So:

```css
.navbar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 24px;
}
```

Means:

```text
justify-content: center = center items horizontally
align-items: center     = center items vertically
```

Example with height:

```css
.navbar {
  height: 80px;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 24px;
}
```

Visual:

```text
+--------------------------------------+
|          Home  About  Contact        |
+--------------------------------------+
```

`justify-content` moves the links to the horizontal center.

`align-items` centers the links vertically inside the `80px` navbar height.

## When flex-direction Is column

If the direction changes to column, the axes switch.

```css
.menu {
  height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
```

Now:

```text
main axis  = vertical
cross axis = horizontal
```

So:

```text
justify-content: center = center items vertically
align-items: center     = center items horizontally
```

Visual:

```text
+----------------------+
|                      |
|        Home          |
|        About         |
|        Contact       |
|                      |
+----------------------+
```

Interview answer: `justify-content` aligns flex items along the main axis, while `align-items` aligns them along the cross axis. The main axis depends on `flex-direction`.

Example: button row

```html
<div class="actions">
  <button>Cancel</button>
  <button>Save</button>
</div>
```

```css
.actions {
  display: flex;
  justify-content: flex-end;
  gap: 12px;
}
```

Visual:

```text
                         [Cancel] [Save]
```

Interview explanation: I use Flexbox for one-dimensional alignment, such as navbars, button groups, toolbars, and centering content.

## display: grid

Grid is a two-dimensional layout system. It controls rows and columns together.

Example: dashboard cards

```html
<section class="dashboard">
  <div>Users</div>
  <div>Revenue</div>
  <div>Orders</div>
</section>
```

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

Visual:

```text
+----------+ +----------+ +----------+
| Users    | | Revenue  | | Orders   |
+----------+ +----------+ +----------+
```

Responsive example:

```css
.dashboard {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 768px) {
  .dashboard {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

Interview explanation: I use Grid for page layouts, dashboards, galleries, and places where both row and column structure matter.

## CSS Grid Detailed Explanation

CSS Grid is used when you want to control layout in two directions:

```text
rows    = horizontal tracks
columns = vertical tracks
```

Simple idea:

```text
Flexbox = one direction at a time
Grid    = rows and columns together
```

## Grid Visual Diagram

```text
Grid container
+-------------+-------------+-------------+
|  column 1   |  column 2   |  column 3   |
+-------------+-------------+-------------+
|  column 1   |  column 2   |  column 3   |
+-------------+-------------+-------------+
```

The parent becomes the grid container:

```css
.dashboard {
  display: grid;
}
```

The children become grid items:

```html
<section class="dashboard">
  <div>Users</div>
  <div>Revenue</div>
  <div>Orders</div>
</section>
```

## Example 1. Three Equal Columns

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

This means:

```text
repeat(3, 1fr) = create 3 equal columns
1fr            = one fraction of available space
gap: 16px      = space between grid items
```

Visual:

```text
+----------+ 16px +----------+ 16px +----------+
| Users    |     | Revenue  |     | Orders   |
+----------+     +----------+     +----------+
```

If the container has `900px` available width and the gap takes `32px` total:

```text
available for columns = 900px - 32px
available for columns = 868px
each column           = 868px / 3
```

Why gap is `32px`:

```text
3 columns create 2 spaces between them
gap = 16px
total gap = 16px + 16px = 32px
```

Step-by-step:

```text
container width = 900px
columns         = 3
gap between columns = 16px
number of gaps  = 2
total gap space = 32px
remaining width = 900px - 32px = 868px
each 1fr column = 868px / 3 = 289.33px
```

Visual with rough sizes:

```text
900px container
+----------------+ 16px +----------------+ 16px +----------------+
| 289.33px       |      | 289.33px       |      | 289.33px       |
| Users          |      | Revenue        |      | Orders         |
+----------------+      +----------------+      +----------------+
```

Important: `gap` is not inside the cards. It is the space between the grid columns and rows.

```text
card padding = space inside each card
grid gap     = space between cards
```

Example with card padding:

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.dashboard > div {
  padding: 20px;
  border: 1px solid #d1d5db;
}
```

Here:

```text
gap: 16px   = space between Users, Revenue, Orders cards
padding: 20px = space inside each card
```

Simple interview explanation: `repeat(3, 1fr)` means make three equal columns. The browser first removes the gap space, then divides the remaining space equally among the three columns.

Interview explanation: `fr` divides available space after fixed widths and gaps are considered.

## Example 2. Responsive Card Grid

Mobile-first approach:

```css
.dashboard {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 768px) {
  .dashboard {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

On mobile:

```text
+----------+
| Users    |
+----------+
| Revenue  |
+----------+
| Orders   |
+----------+
```

On desktop:

```text
+----------+ +----------+ +----------+
| Users    | | Revenue  | | Orders   |
+----------+ +----------+ +----------+
```

Interview explanation: I usually start with one column for mobile, then use media queries to create multiple columns for larger screens.

## Example 3. 60/40 Layout

Grid is very useful for page layouts like content plus sidebar.

```html
<main class="page-layout">
  <section class="main-content">Main Content</section>
  <aside class="sidebar">Sidebar</aside>
</main>
```

```css
.page-layout {
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 24px;
}
```

`3fr 2fr` creates a 60/40 style layout.

```text
3fr + 2fr = 5 parts
main content = 3 parts = 60%
sidebar      = 2 parts = 40%
```

Visual:

```text
+------------------------------+--------------------+
|        Main Content          |      Sidebar       |
|            60%               |        40%         |
+------------------------------+--------------------+
```

Responsive version:

```css
.page-layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

@media (min-width: 900px) {
  .page-layout {
    grid-template-columns: 3fr 2fr;
  }
}
```

Interview explanation: I prefer `3fr 2fr` over hardcoded `60% 40%` because fractions adapt cleanly with available space and gaps.

## Example 4. Fixed Sidebar And Flexible Content

```css
.app-layout {
  display: grid;
  grid-template-columns: 240px 1fr;
  min-height: 100vh;
}
```

This means:

```text
sidebar = fixed 240px
content = remaining available space
```

Visual:

```text
+----------+--------------------------------+
| Sidebar  | Main Content                   |
| 240px    | remaining width                |
+----------+--------------------------------+
```

Realtime use cases:

```text
admin dashboard
CRM layout
settings page
documentation layout
```

## What min-height: 100vh Means

```css
min-height: 100vh;
```

This means the element should be at least as tall as the full visible browser height.

Breakdown:

```text
min-height = minimum height
100vh      = 100% of viewport height
```

The viewport is the visible area of the browser window.

Example:

```text
browser viewport height = 800px
100vh                   = 800px
```

So if `.app-layout` has:

```css
.app-layout {
  min-height: 100vh;
}
```

Then `.app-layout` will be at least `800px` tall on that screen.

Visual:

```text
Viewport height
+-----------------------------+
| app-layout starts here      |
|                             |
| fills at least full screen  |
|                             |
| app-layout ends here        |
+-----------------------------+
```

## height: 100vh vs min-height: 100vh

`height: 100vh` forces the element to be exactly the viewport height.

```css
.page {
  height: 100vh;
}
```

If content is taller than the screen, it may overflow.

`min-height: 100vh` sets a minimum height but still allows the element to grow if content needs more space.

```css
.page {
  min-height: 100vh;
}
```

Example:

```text
viewport height = 800px
content height  = 1200px
```

With `min-height: 100vh`, the element can grow to `1200px`.

Interview explanation: `min-height: 100vh` is commonly used for full-page layouts because it makes the layout cover the full screen while still allowing content to grow naturally.

Interview explanation: Grid is a good choice when one area has a fixed size and another area should fill the remaining space.

## Example 5. Header, Sidebar, And Content Layout

```html
<div class="app-shell">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Content</main>
</div>
```

```css
.app-shell {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 64px 1fr;
  grid-template-areas:
    "header header"
    "sidebar content";
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}
```

Visual:

```text
+-------------------------------------------+
| Header                                    |
+------------+------------------------------+
| Sidebar    | Content                      |
|            |                              |
+------------+------------------------------+
```

Interview explanation: `grid-template-areas` makes large page layouts readable because the CSS visually describes the page structure.

## How grid-template-areas Works

`grid-template-areas` lets you name parts of a grid layout using words.

In this example:

```css
.app-shell {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 64px 1fr;
  grid-template-areas:
    "header header"
    "sidebar content";
}
```

The layout has:

```text
2 columns
2 rows
```

Because:

```css
grid-template-columns: 240px 1fr;
```

means:

```text
column 1 = 240px
column 2 = remaining space
```

And:

```css
grid-template-rows: 64px 1fr;
```

means:

```text
row 1 = 64px
row 2 = remaining height
```

Now look at the area names:

```css
grid-template-areas:
  "header header"
  "sidebar content";
```

Visual meaning:

```text
row 1: header  header
row 2: sidebar content
```

Diagram:

```text
+----------------+-----------------------------+
| header         | header                      |
+----------------+-----------------------------+
| sidebar        | content                     |
+----------------+-----------------------------+
```

The word `header` appears in both columns of the first row, so the header spans across the full width.

```text
"header header" = header takes column 1 and column 2
```

The second row has two different areas:

```text
"sidebar content" = sidebar on left, content on right
```

Then each child element is placed into one named area:

```css
.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}
```

This means:

```text
.header goes into the header area
.sidebar goes into the sidebar area
.content goes into the content area
```

## Step-by-step Real Example

HTML:

```html
<div class="app-shell">
  <header class="header">Admin Panel</header>
  <aside class="sidebar">Menu</aside>
  <main class="content">Dashboard Content</main>
</div>
```

CSS:

```css
.app-shell {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-rows: 64px 1fr;
  grid-template-areas:
    "header header"
    "sidebar content";
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}
```

Final layout:

```text
+------------------------------------------------+
| Admin Panel                                    |
+---------------+--------------------------------+
| Menu          | Dashboard Content              |
|               |                                |
|               |                                |
+---------------+--------------------------------+
```

## Why This Is Useful

Without `grid-template-areas`, you may need to place items using line numbers:

```css
.header {
  grid-column: 1 / 3;
  grid-row: 1;
}
```

That works, but it is less readable for large layouts.

With named areas:

```css
.header {
  grid-area: header;
}
```

The CSS becomes easier to understand because the layout looks like a simple map.

## Responsive Example

On mobile, you may want the layout to stack:

```text
header
sidebar
content
```

CSS:

```css
.app-shell {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto;
  grid-template-areas:
    "header"
    "sidebar"
    "content";
}

@media (min-width: 768px) {
  .app-shell {
    grid-template-columns: 240px 1fr;
    grid-template-rows: 64px 1fr;
    grid-template-areas:
      "header header"
      "sidebar content";
  }
}
```

Mobile visual:

```text
+----------------------+
| Header               |
+----------------------+
| Sidebar              |
+----------------------+
| Content              |
+----------------------+
```

Desktop visual:

```text
+-------------------------------------------+
| Header                                    |
+------------+------------------------------+
| Sidebar    | Content                      |
+------------+------------------------------+
```

Best interview answer: `grid-template-areas` lets us create named layout regions in CSS. Each string represents a row, and each word represents a column area. Repeating the same area name makes that area span multiple columns or rows. It is very useful for readable page layouts like header, sidebar, and main content.

## Making This Layout Responsive

For this layout:

```css
grid-template-columns: 240px 1fr;
grid-template-rows: 64px 1fr;
```

The desktop structure is:

```text
header  = 64px height
sidebar = 240px width
content = remaining space
```

Desktop visual:

```text
+-------------------------------------------+
| Header: 64px                              |
+------------+------------------------------+
| Sidebar    | Content                      |
| 240px      | remaining width              |
+------------+------------------------------+
```

On mobile, a fixed `240px` sidebar may take too much horizontal space. So a common responsive solution is to stack the layout.

Mobile visual:

```text
+----------------------+
| Header               |
+----------------------+
| Sidebar/Menu         |
+----------------------+
| Content              |
+----------------------+
```

## Responsive Grid Solution

Use mobile-first CSS.

Start with one column:

```css
.app-shell {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto auto 1fr;
  grid-template-areas:
    "header"
    "sidebar"
    "content";
}
```

Meaning:

```text
grid-template-columns: 1fr = one full-width column
grid-template-rows: auto auto 1fr = header auto, sidebar auto, content remaining
```

## What @media (min-width: 768px) Means

```css
@media (min-width: 768px) {
  .app-shell {
    grid-template-columns: 240px 1fr;
  }
}
```

This does not mean mobile view.

It means:

```text
Apply these styles when the viewport width is 768px or bigger.
```

So:

```text
390px mobile        = media query does not apply
600px mobile/tablet = media query does not apply
768px tablet        = media query applies
1024px desktop      = media query applies
1440px desktop      = media query applies
```

This is called mobile-first CSS because the default styles are written for mobile first, outside the media query.

```css
.app-shell {
  grid-template-columns: 1fr;
}
```

Then larger-screen styles are added inside `min-width`.

```css
@media (min-width: 768px) {
  .app-shell {
    grid-template-columns: 240px 1fr;
  }
}
```

Simple memory trick:

```text
min-width = from this width and above
max-width = up to this width and below
```

Example with `max-width`:

```css
@media (max-width: 767px) {
  .sidebar {
    display: none;
  }
}
```

This means:

```text
Apply styles only when viewport width is 767px or smaller.
```

Best interview answer: `@media (min-width: 768px)` means the styles apply from `768px` and above, usually tablet and desktop sizes. In mobile-first CSS, mobile styles are written as the default, and larger-screen styles are added using `min-width` media queries.

Then switch to desktop layout at a larger screen size:

```css
@media (min-width: 768px) {
  .app-shell {
    grid-template-columns: 240px 1fr;
    grid-template-rows: 64px 1fr;
    grid-template-areas:
      "header header"
      "sidebar content";
  }
}
```

Full example:

```html
<div class="app-shell">
  <header class="header">Header</header>
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Content</main>
</div>
```

```css
.app-shell {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto auto 1fr;
  grid-template-areas:
    "header"
    "sidebar"
    "content";
}

.header {
  grid-area: header;
}

.sidebar {
  grid-area: sidebar;
}

.content {
  grid-area: content;
}

@media (min-width: 768px) {
  .app-shell {
    grid-template-columns: 240px 1fr;
    grid-template-rows: 64px 1fr;
    grid-template-areas:
      "header header"
      "sidebar content";
  }
}
```

Interview explanation: I would use mobile-first Grid. On small screens, I stack header, sidebar, and content. On larger screens, I switch to a two-column layout with a fixed sidebar and flexible content area.

## Can We Make It Responsive With Flexbox?

Yes. Flexbox can also make a sidebar/content layout responsive using:

```text
flex-basis
flex-grow
flex-shrink
flex-wrap
media queries
```

But Flexbox is one-dimensional, so it is usually simpler for just sidebar plus content. Grid is usually clearer when the layout has header, sidebar, and content areas together.

## Flexbox Responsive Sidebar Example

HTML:

```html
<div class="layout">
  <aside class="sidebar">Sidebar</aside>
  <main class="content">Content</main>
</div>
```

CSS:

```css
.layout {
  min-height: 100vh;
  display: flex;
  flex-wrap: wrap;
}

.sidebar {
  flex: 0 0 240px;
}

.content {
  flex: 1 1 300px;
}
```

Breakdown:

```text
flex-wrap: wrap = allow items to move to next line when space is not enough
```

For sidebar:

```css
flex: 0 0 240px;
```

Means:

```text
flex-grow: 0   = do not grow
flex-shrink: 0 = do not shrink
flex-basis: 240px = start at 240px
```

For content:

```css
flex: 1 1 300px;
```

Means:

```text
flex-grow: 1   = take remaining space
flex-shrink: 1 = shrink when needed
flex-basis: 300px = preferred starting width
```

Desktop visual:

```text
+----------+-------------------------------+
| Sidebar  | Content                       |
| 240px    | flexible remaining space      |
+----------+-------------------------------+
```

Small screen visual when wrapping happens:

```text
+----------------------+
| Sidebar              |
+----------------------+
| Content              |
+----------------------+
```

## Does flex-shrink Alone Make It Responsive?

No. `flex-shrink` alone only controls whether an item is allowed to become smaller when there is not enough space.

Example:

```css
.sidebar {
  flex-basis: 240px;
  flex-shrink: 1;
}
```

This allows the sidebar to shrink below `240px`.

But the result may be bad:

```text
Sidebar becomes too narrow
text may wrap badly
content may feel squeezed
```

So `flex-shrink` helps with flexibility, but it does not automatically create a good mobile layout.

Better:

```css
.layout {
  display: flex;
  flex-wrap: wrap;
}

.sidebar {
  flex: 0 0 240px;
}

.content {
  flex: 1 1 300px;
}
```

This lets the content wrap below when the screen becomes too narrow.

## Flexbox With Media Query

For a more controlled mobile layout:

```css
.layout {
  min-height: 100vh;
  display: flex;
}

.sidebar {
  flex: 0 0 240px;
}

.content {
  flex: 1 1 auto;
}

@media (max-width: 767px) {
  .layout {
    flex-direction: column;
  }

  .sidebar {
    flex-basis: auto;
    width: 100%;
  }

  .content {
    width: 100%;
  }
}
```

Mobile result:

```text
+----------------------+
| Sidebar/Menu         |
+----------------------+
| Content              |
+----------------------+
```

Desktop result:

```text
+----------+-------------------------------+
| Sidebar  | Content                       |
+----------+-------------------------------+
```

Interview answer: Yes, we can make a layout responsive with Flexbox using `flex-wrap`, `flex-basis`, `flex-grow`, and `flex-shrink`. But `flex-shrink` alone is not enough; it only allows items to shrink. For a clean responsive layout, I usually combine flexible `flex` values with `flex-wrap` or use media queries to switch from row layout to column layout.

## Example 6. auto-fit And minmax

This is useful for responsive card grids without writing many breakpoints.

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}
```

Meaning:

```text
auto-fit        = create as many columns as fit
minmax(220px, 1fr) = each card is at least 220px, then grows if space is available
```

Visual on wide screen:

```text
+--------+ +--------+ +--------+ +--------+
| Card   | | Card   | | Card   | | Card   |
+--------+ +--------+ +--------+ +--------+
```

Visual on small screen:

```text
+--------+
| Card   |
+--------+
| Card   |
+--------+
```

Interview explanation: `repeat(auto-fit, minmax())` is a strong responsive Grid pattern because the browser automatically decides how many columns can fit.

## Grid vs Flexbox Interview Difference

Use Flexbox when alignment is mainly one-dimensional:

```css
.toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

Use Grid when the layout needs rows and columns:

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

Simple answer:

```text
Flexbox = row or column alignment
Grid    = rows and columns layout
```

Best interview answer: CSS Grid is a two-dimensional layout system used to control rows and columns together. I use Grid for dashboards, page shells, card grids, galleries, and content/sidebar layouts. Flexbox is better for one-dimensional alignment like navbars, toolbars, and button groups.

## display: none

`display: none` removes the element from the layout completely.

```html
<div class="alert">Saved successfully</div>
```

```css
.alert {
  display: none;
}
```

Result:

```text
element is hidden
element does not take space
nearby elements move as if it does not exist
```

## Realtime Uses Of display: none

`display: none` is useful when the element should completely disappear from the page layout.

## Example 1. Hide And Show Mobile Menu

```html
<button class="menu-button">Menu</button>

<nav class="mobile-menu">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</nav>
```

```css
.mobile-menu {
  display: none;
}

.mobile-menu.open {
  display: block;
}
```

Explanation:

```text
default state = menu is hidden
open state    = menu becomes visible
```

This is common for hamburger menus. JavaScript usually adds or removes the `.open` class when the user clicks the menu button.

## Example 2. Hide Modal Before Opening

```html
<div class="modal">
  <div class="modal-content">
    <h2>Confirm Delete</h2>
    <button>Cancel</button>
    <button>Delete</button>
  </div>
</div>
```

```css
.modal {
  display: none;
}

.modal.is-open {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Explanation:

```text
display: none = modal is hidden and takes no space
display: flex = modal is visible and its content can be centered
```

This is useful for login popups, confirmation dialogs, image previews, and alert dialogs.

## Example 3. Switch Desktop And Mobile Navigation

```html
<nav class="desktop-nav">Desktop Navigation</nav>
<nav class="mobile-nav">Mobile Navigation</nav>
```

```css
.desktop-nav {
  display: block;
}

.mobile-nav {
  display: none;
}

@media (max-width: 767px) {
  .desktop-nav {
    display: none;
  }

  .mobile-nav {
    display: block;
  }
}
```

Explanation:

```text
desktop screen = show desktop nav, hide mobile nav
mobile screen  = hide desktop nav, show mobile nav
```

This is common when desktop and mobile navigation have very different structures.

## Example 4. Hide Form Error Message Until Needed

```html
<div class="form-field">
  <label>Email</label>
  <input type="email">
  <p class="error-message">Email is required</p>
</div>
```

```css
.error-message {
  display: none;
}

.form-field.has-error .error-message {
  display: block;
}
```

Explanation:

```text
normal field = error message hidden
error field  = error message visible
```

This is useful for validation messages that should appear only after an error.

## Example 5. Conditional UI Sections

```html
<section class="empty-state">No data found</section>
<section class="results-list">Results go here</section>
```

```css
.empty-state {
  display: none;
}

.page.is-empty .empty-state {
  display: block;
}

.page.is-empty .results-list {
  display: none;
}
```

Explanation:

```text
when data exists = show results
when no data     = hide results and show empty state
```

This is common in dashboards, search pages, tables, and product lists.

## Important Accessibility Note

Elements with `display: none` are hidden visually and are also not available to screen readers.

Use `display: none` when the content should truly be unavailable.

If content should be visually hidden but still available to screen readers, use a visually-hidden utility instead.

Interview answer: `display: none` is helpful when an element should be hidden and removed from layout, such as mobile menus before opening, modals before showing, form errors before validation, desktop/mobile UI switching, and conditional empty states.

Interview explanation: I use `display: none` when an element should be hidden and should not occupy layout space.

## block vs inline vs inline-block

```text
block:
- starts on a new line
- takes full available width
- width and height work

inline:
- stays in text flow
- takes only content width
- width and height do not work normally

inline-block:
- stays inline
- width, height, padding, and margin work more predictably
```

Interview example:

```html
<span class="badge">New</span>
```

```css
.badge {
  display: inline-block;
  padding: 4px 8px;
  border-radius: 4px;
}
```

I would use `inline-block` here because a badge should stay inline with text but still have padding like a box.

## Difference Between block And inline-block

Both `block` and `inline-block` elements behave like boxes, but they sit differently in the page layout.

## display: block Example

```html
<div class="box">One</div>
<div class="box">Two</div>
<div class="box">Three</div>
```

```css
.box {
  display: block;
  width: 200px;
  padding: 12px;
  border: 1px solid #2563eb;
  margin-bottom: 8px;
}
```

Visual:

```text
+----------------+
| One            |
+----------------+

+----------------+
| Two            |
+----------------+

+----------------+
| Three          |
+----------------+
```

Even though each box has `width: 200px`, each block element starts on a new line.

Important behavior:

```text
block = starts on a new line
block = takes full available width by default
block = width and height work
block = elements stack vertically
```

Realtime examples:

```text
div
section
article
card
paragraph
page container
form field row
```

Interview explanation: I use `block` when an element should behave like a section or container and naturally stack with other elements.

## display: inline-block Example

```html
<span class="tag">HTML</span>
<span class="tag">CSS</span>
<span class="tag">JavaScript</span>
```

```css
.tag {
  display: inline-block;
  padding: 6px 12px;
  border: 1px solid #d1d5db;
  margin: 4px;
}
```

Visual:

```text
[ HTML ] [ CSS ] [ JavaScript ]
```

The elements stay side by side, but they still accept padding, margin, width, and height more predictably.

Important behavior:

```text
inline-block = stays in the same line if space is available
inline-block = takes only needed content width by default
inline-block = width and height work
inline-block = useful for small UI pieces
```

Realtime examples:

```text
badges
tags
chips
small labels
inline buttons
pill-shaped status indicators
```

Interview explanation: I use `inline-block` when I want an element to stay inline with other elements but still behave like a box.

## Width Difference

Block elements take full available width by default.

```html
<div class="block-box">Block Box</div>
```

```css
.block-box {
  display: block;
  border: 1px solid #2563eb;
}
```

Visual:

```text
+--------------------------------------+
| Block Box                            |
+--------------------------------------+
```

Inline-block elements take only the width needed by their content by default.

```html
<span class="inline-box">Inline Block</span>
```

```css
.inline-box {
  display: inline-block;
  border: 1px solid #2563eb;
}
```

Visual:

```text
[ Inline Block ]
```

If you set a width, both can use it:

```css
.block-box,
.inline-box {
  width: 200px;
}
```

Difference:

```text
block        = 200px wide but still starts on a new line
inline-block = 200px wide and can still sit beside other inline/inline-block elements
```

## Simple Interview Answer

`block` elements start on a new line and take the full available width by default. `inline-block` elements stay side by side like inline elements, but they also support width, height, padding, and margin like block elements. I use `block` for layout sections and containers, and `inline-block` for badges, tags, chips, and small UI elements that should appear in one line.

## position: static

`static` is the default position for HTML elements.

```css
.box {
  position: static;
}
```

With `static`, the element stays in normal document flow. Properties like `top`, `right`, `bottom`, and `left` do not affect it.

```css
.box {
  position: static;
  top: 20px;
}
```

Here `top: 20px` does not move the element.

## What Is The Use Of top: 20px?

`top: 20px` is an offset property. It tells the browser to move or place an element `20px` from the top, but it only works when the element has a position value that supports offsets.

These properties are called offset properties:

```text
top
right
bottom
left
```

Important:

```text
top does not work with position: static
top works with position: relative, absolute, fixed, and sticky
```

## Example 1. top With position: static

```html
<div class="box">Static Box</div>
```

```css
.box {
  position: static;
  top: 20px;
}
```

Result:

```text
The box does not move.
```

Why:

```text
static is normal document flow
offset properties do not affect static elements
```

So in this example, `top: 20px` is useless. It is shown only to explain that `top` does not work with `position: static`.

## Example 2. top With position: relative

```css
.box {
  position: relative;
  top: 20px;
}
```

Result:

```text
The box moves 20px down from its original position.
Its original space is still reserved.
```

Visual:

```text
Original position:
+-------------+
| Box         |
+-------------+

After top: 20px:

  20px down
     +-------------+
     | Box         |
     +-------------+
```

Interview explanation: With `relative`, `top: 20px` moves the element down visually, but the layout still remembers its original position.

## Example 3. top With position: absolute

```html
<div class="card">
  <span class="badge">New</span>
</div>
```

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 20px;
  right: 20px;
}
```

Result:

```text
The badge is placed 20px from the top of the card
and 20px from the right of the card.
```

Visual:

```text
+--------------------------------+
|                    20px [New]  |
|                                |
| Card content                   |
+--------------------------------+
```

Interview explanation: With `absolute`, `top: 20px` places the element 20px from the top edge of its nearest positioned ancestor.

## Example 4. top With position: fixed

```css
.notification {
  position: fixed;
  top: 20px;
  right: 20px;
}
```

Result:

```text
The notification stays 20px from the top of the browser viewport.
```

Realtime use cases:

```text
toast notifications
fixed header
floating chat button
modal close button
```

## Best Interview Answer

`top: 20px` is used to offset or place a positioned element from the top. It has no effect on `position: static`. With `relative`, it moves the element down from its original position. With `absolute`, it places the element from the top of the nearest positioned ancestor. With `fixed`, it places the element from the top of the viewport.

Interview explanation: Static is the default. I usually do not write it unless I need to reset another position value.

## position: relative

`relative` keeps the element in normal flow, but allows it to be shifted visually from its original position.

Example:

```html
<span class="badge">New</span>
```

```css
.badge {
  position: relative;
  top: -4px;
}
```

Visual idea:

```text
Original space is still reserved.
The element is visually moved from that original spot.
```

Important:

```text
position: relative does not remove the element from layout
```

Realtime example: slightly moving a badge, icon, label, or tooltip arrow.

Interview explanation: I use `relative` when I need a small visual adjustment or when I need the element to become the reference point for an absolutely positioned child.

## position: absolute

`absolute` removes the element from normal document flow.

It is positioned relative to the nearest ancestor whose position is not `static`.

Example: badge inside a card

```html
<div class="card">
  <span class="badge">New</span>
  <h3>Account</h3>
</div>
```

```css
.card {
  position: relative;
  padding: 24px;
  border: 1px solid #d1d5db;
}

.badge {
  position: absolute;
  top: 12px;
  right: 12px;
}
```

Visual:

```text
+--------------------------------+
|                         [New]  |
| Account                        |
+--------------------------------+
```

Why `.card` has `position: relative`:

```text
It creates the positioning context for .badge.
```

Without `position: relative` on `.card`, the badge may position itself relative to another ancestor or the page.

Interview explanation: I use `absolute` for badges, overlays, dropdowns, icons inside inputs, and elements that should be placed relative to a container.

## position: fixed

`fixed` positions an element relative to the viewport.

It stays in the same place even when the page scrolls.

Example: fixed header

```html
<header class="site-header">Dashboard</header>
```

```css
.site-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 64px;
}
```

Realtime examples:

```text
sticky-looking top nav
chat button
cookie banner
global notification
modal backdrop
```

Interview explanation: I use `fixed` when an element should stay attached to the viewport regardless of page scroll.

## position: sticky

`sticky` is a mix of `relative` and `fixed`.

The element behaves normally until it reaches a scroll threshold, then it sticks.

Example: sticky filter bar

```html
<div class="filters">Filters</div>
```

```css
.filters {
  position: sticky;
  top: 0;
  background: white;
  z-index: 10;
}
```

Visual behavior:

```text
Before scroll threshold = normal position
After reaching top: 0   = sticks to top of viewport
```

Realtime examples:

```text
table headers
dashboard filters
section navigation
product category bar
```

Interview explanation: I use `sticky` when an element should scroll normally at first but remain visible after reaching a certain point.

## fixed vs sticky

`fixed` and `sticky` can both keep an element visible while scrolling, but their behavior is different.

Simple difference:

```text
fixed  = always attached to the viewport
sticky = scrolls normally first, then sticks after reaching a threshold
```

## position: fixed Visual

```css
.header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
}
```

Before scroll:

```text
+-----------------------------+
| Fixed Header                |
+-----------------------------+
| Page content                |
| Page content                |
| Page content                |
+-----------------------------+
```

After scroll:

```text
+-----------------------------+
| Fixed Header                |  still attached to viewport
+-----------------------------+
| Later page content          |
| Later page content          |
| Later page content          |
+-----------------------------+
```

The fixed element does not scroll away with its parent content. It stays attached to the browser viewport.

Realtime use cases:

```text
global navbar
floating chat button
cookie banner
toast notification
modal backdrop
```

## position: sticky Visual

```css
.filters {
  position: sticky;
  top: 0;
}
```

Initial position:

```text
+-----------------------------+
| Intro content               |
| Intro content               |
| Filter Bar                  |  normal position
| Product list                |
+-----------------------------+
```

After scrolling until the filter reaches `top: 0`:

```text
+-----------------------------+
| Filter Bar                  |  stuck at top
+-----------------------------+
| Product list                |
| Product list                |
| Product list                |
+-----------------------------+
```

When the parent section ends:

```text
+-----------------------------+
| Next section                |  filter bar has scrolled away
| Next section content        |
+-----------------------------+
```

Important: A sticky element is not permanently fixed. It sticks only within its parent or scroll container.

## Does sticky Also Scroll Away?

Yes. A sticky element scrolls normally at first. Then it sticks when it reaches the offset, such as `top: 0`. When its parent container ends, the sticky element scrolls away with that parent.

Behavior:

```text
1. Before reaching top: 0
   sticky element scrolls like normal content

2. When it reaches top: 0
   sticky element sticks to the top of the viewport

3. When its parent/container ends
   sticky element scrolls away
```

Example:

```html
<section class="products-section">
  <div class="filters">Filters</div>
  <div class="products">Products...</div>
</section>

<section class="reviews-section">
  Reviews...
</section>
```

```css
.filters {
  position: sticky;
  top: 0;
}
```

Here, `.filters` can stick while the user scrolls inside the products section. But when the products section finishes and the reviews section reaches the viewport, the filter bar scrolls away.

## Fixed vs Sticky Table

```text
fixed:
- relative to viewport
- removed from normal flow
- always stays in the same viewport position
- does not stop when parent ends
- useful for global UI

sticky:
- relative to scroll position and parent container
- stays in normal flow at first
- sticks only after reaching top/right/bottom/left offset
- scrolls away when parent container ends
- useful for section-level UI
```

Best interview answer: `fixed` positions an element relative to the viewport and keeps it there all the time. `sticky` behaves like a normal element first, then becomes fixed-like after reaching a scroll threshold such as `top: 0`. Unlike fixed, sticky is limited by its parent or scroll container, so it can scroll away when that container ends.

## relative vs absolute

```text
relative:
- stays in normal flow
- original space remains
- can be shifted from original position
- can create a reference point for absolute children

absolute:
- removed from normal flow
- does not reserve original space
- positioned relative to nearest positioned ancestor
```

Example:

```css
.card {
  position: relative;
}

.card .badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```

Interview answer: `relative` is often used on the parent, and `absolute` is used on the child that needs exact placement inside that parent.

## Real Interview Scenario

Question: How would you place a search icon inside an input?

```html
<div class="search-field">
  <span class="search-icon">Search</span>
  <input type="text" placeholder="Search users">
</div>
```

```css
.search-field {
  position: relative;
}

.search-icon {
  position: absolute;
  left: 12px;
  top: 50%;
  transform: translateY(-50%);
}

.search-field input {
  padding-left: 40px;
}
```

Explanation:

```text
.search-field position: relative = reference container
.search-icon position: absolute  = place icon inside container
top: 50% + transform             = vertically center icon
padding-left on input            = prevents text from overlapping icon
```

## Resume-Based Example

Use `sticky` for a dashboard filter bar, `absolute` for small badges inside cards, and `fixed` for global notifications or modals.

## Interview Answer

Display defines layout behavior. Position defines placement behavior. I use `block` for stacked sections, `inline` for text-level elements, `inline-block` for badges, Flexbox for one-dimensional alignment, and Grid for two-dimensional layouts. For positioning, I use `relative` to keep an element in flow or create a reference point, `absolute` for elements placed inside a container, `fixed` for viewport-based UI, and `sticky` for scroll-aware headers or filter bars.
