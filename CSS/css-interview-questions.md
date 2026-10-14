# CSS Interview Questions Quick Review

Use this before interviews for fast revision. The examples relate to frontend dashboards, onboarding flows, forms, and component-based React UI.

## 1. What Is CSS?

CSS stands for Cascading Style Sheets. It controls the visual presentation of HTML, including layout, colors, spacing, typography, and responsive behavior.

Example:

```css
.status-card {
  padding: 16px;
  border: 1px solid #d0d7de;
  border-radius: 8px;
}
```

## 2. What Is The CSS Cascade?

The cascade decides which CSS rule wins when multiple rules target the same element.

Priority order:

```text
Importance -> specificity -> source order
```

`!important` has high priority, but overusing it makes CSS hard to maintain.

## 3. What Is Specificity?

Specificity is the weight of a selector.

Diagram:

```text
inline styles      highest
IDs                high
classes/attributes medium
elements           low
```

Example:

```css
#submit { color: red; }
.button { color: blue; }
button { color: green; }
```

The ID selector wins.

## 4. Difference Between class And id In CSS?

`id` should be unique and has higher specificity. `class` is reusable and preferred for styling.

Interview answer: I use classes for reusable component styles and IDs mainly for anchors or accessibility relationships.

## 5. What Is The Box Model?

Every element is treated as a box.

Diagram:

```text
margin
  border
    padding
      content
```

Example:

```css
.card {
  width: 300px;
  padding: 16px;
  border: 1px solid #ccc;
  margin: 12px;
  box-sizing: border-box;
}
```

## 6. What Is box-sizing: border-box?

`border-box` includes padding and border inside the declared width and height.

Interview answer: I commonly use `box-sizing: border-box` because it makes layout sizing predictable.

## 7. Difference Between block, inline, And inline-block?

Block starts on a new line and takes available width. Inline stays in text flow. Inline-block stays inline but accepts width and height.

The broader `display` property controls how an element participates in layout:

| Value | Behavior | Typical use |
| --- | --- | --- |
| `block` | Starts on a new line and normally fills available width | Sections and containers |
| `inline` | Flows with text; normal `width` and `height` do not apply | Links and text spans |
| `inline-block` | Flows inline but accepts box dimensions | Badges and compact controls |
| `flex` | Creates a one-dimensional flex formatting context for children | Toolbars and component alignment |
| `grid` | Creates a two-dimensional grid formatting context for children | Dashboards and page layouts |
| `none` | Removes the element from layout and the accessibility tree | Content that is currently unavailable |

```css
.onboarding-actions {
  display: flex;
  gap: 0.75rem;
}
```

## 8. Difference Between relative, absolute, fixed, And sticky Positioning?

`relative` moves relative to itself. `absolute` positions relative to the nearest positioned ancestor. `fixed` positions relative to the viewport. `sticky` behaves like relative until a scroll threshold, then sticks.

`static` is the default and ignores inset properties such as `top` and `left`. `relative` remains in normal flow, while `absolute` and `fixed` are removed from normal flow. A sticky element remains in flow.

```text
static   -> normal document flow
relative -> normal flow + offset; can anchor an absolute child
absolute -> nearest positioned ancestor
fixed    -> viewport
sticky   -> scroll container until an inset threshold is reached
```

```css
.application-card {
  position: relative;
}

.status-badge {
  position: absolute;
  inset-block-start: 0.75rem;
  inset-inline-end: 0.75rem;
}

.page-header {
  position: sticky;
  top: 0;
}
```

Interview answer: I choose positioning according to the containing block and whether the element should remain in document flow. For example, I use an absolute badge inside a relative card and a sticky header for long onboarding forms.

## 9. What Is Flexbox?

Flexbox is a one-dimensional layout system for arranging items in a row or column.

Example:

```css
.toolbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
```

Use it for nav bars, toolbars, card actions, and alignment.

## 10. What Is CSS Grid?

Grid is a two-dimensional layout system for rows and columns.

Example:

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

Use it for dashboards, page layouts, and complex card grids.

## 11. Flexbox vs Grid?

```text
Flexbox = one dimension, row or column
Grid    = two dimensions, rows and columns
```

Interview answer: I use Flexbox for alignment and small component layouts. I use Grid for full page or dashboard layouts.

## 12. What Are Media Queries?

Media queries apply styles based on screen size, device features, or user preferences.

Example:

```css
@media (max-width: 768px) {
  .dashboard {
    grid-template-columns: 1fr;
  }
}
```

## 13. Mobile-First vs Desktop-First CSS?

Mobile-first starts with small-screen styles, then adds larger-screen styles with `min-width`.

Example:

```css
.cards { display: grid; grid-template-columns: 1fr; }

@media (min-width: 768px) {
  .cards { grid-template-columns: repeat(3, 1fr); }
}
```

## 14. What CSS Units Do You Use?

Common units:

- `px`: fixed size
- `%`: relative to parent
- `em`: relative to current font size
- `rem`: relative to root font size
- `vw`/`vh`: viewport width/height
- `fr`: grid fraction unit

## 15. What Is rem?

`rem` is relative to the root element font size. It is useful for scalable spacing and typography.

## 16. What Are CSS Variables?

CSS variables store reusable values.

Example:

```css
:root {
  --color-primary: #0f766e;
  --space-md: 16px;
}

.button {
  background: var(--color-primary);
  padding: var(--space-md);
}
```

Interview answer: CSS variables are useful for theming, design tokens, and consistent component styling.

## 17. What Is Responsive Design?

Responsive design makes UI adapt to different screen sizes and devices.

Interview answer: I use fluid layouts, flexible images, media queries, relative units, and mobile-first CSS to create responsive experiences.

## 18. How Do You Make CSS Accessible?

Use visible focus states, sufficient color contrast, readable font sizes, avoid motion-heavy UI, and do not rely on color alone.

Example:

```css
button:focus-visible {
  outline: 3px solid #2563eb;
  outline-offset: 3px;
}
```

## 19. What Is :focus-visible?

`:focus-visible` applies focus styling when the browser determines a visible focus indicator is needed, usually for keyboard navigation.

## 20. What Are Pseudo-classes?

Pseudo-classes style an element in a specific state.

Examples: `:hover`, `:focus`, `:checked`, `:disabled`, `:nth-child()`.

## 21. What Are Pseudo-elements?

Pseudo-elements style a specific part of an element.

Examples: `::before`, `::after`, `::placeholder`, `::first-line`.

## 22. What Is z-index?

`z-index` controls stacking order for positioned elements. It works within stacking contexts.

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
  z-index: 1;
}

.blue {
  z-index: 2;
}
```

The blue box appears above the red box because `z-index: 2` is higher than `z-index: 1`.

Interview answer: `z-index` controls which overlapping element appears in front. It is useful for modals, dropdowns, tooltips, badges, sticky headers, and overlays. If it does not work as expected, I check parent stacking contexts.

## 23. What Is A Stacking Context?

A stacking context is a group of elements stacked together independently from other groups.

Common triggers include `position` with `z-index`, `opacity` less than 1, `transform`, `filter`, and `isolation`.

## 24. What Is The Difference Between visibility: hidden And display: none?

`display: none` removes the element from layout. `visibility: hidden` hides it but keeps its layout space.

## 25. Difference Between opacity: 0, visibility: hidden, And display: none?

```text
opacity: 0          invisible, still takes space, may receive events
visibility: hidden  invisible, still takes space, not normally interactive
display: none       removed from layout
```

## 26. What Are Transitions?

Transitions animate changes between two states.

Example:

```css
.button {
  transition: background-color 200ms ease, transform 200ms ease;
}

.button:hover {
  transform: translateY(-2px);
}
```

## 27. What Are Animations?

Animations use `@keyframes` to define multiple steps.

Example:

```css
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}
```

## 28. How Do You Handle Reduced Motion?

Respect user preferences with `prefers-reduced-motion`.

Example:

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms;
    transition-duration: 0.01ms;
  }
}
```

## 29. What Is The Difference Between margin And padding?

`margin` is space outside the border. `padding` is space inside the border.

```text
<----------- margin: separates this component from others ----------->
  +----------------------------- border ----------------------------+
  |              padding: breathing room inside the card            |
  |        +-------------------- content -------------------+        |
  |        | Application status: Under review              |        |
  |        +------------------------------------------------+        |
  +-----------------------------------------------------------------+
```

```css
.status-card {
  margin-block-end: 1.5rem; /* space between this card and the next */
  padding: 1rem;            /* space between its border and content */
  border: 1px solid #cbd5e1;
}
```

Padding enlarges the element's painted background and contributes to its box size. Margin is transparent, cannot have a background, and vertical margins of normal block elements can collapse. Auto inline margins can center a block with a defined width.

Interview answer: I use padding for internal component spacing and margin for separation between components. In component systems, I often prefer parent `gap` for spacing between children because ownership is clearer and margins do not collapse.

## 30. What Is Margin Collapsing?

Vertical margins between block elements can collapse into one margin. Flex and Grid containers do not have normal margin collapsing between their children.

## 31. What Is BEM?

BEM is a naming convention: Block, Element, Modifier.

Example:

```css
.card {}
.card__title {}
.card--highlighted {}
```

## 32. What Is Utility-First CSS?

Utility-first CSS uses small single-purpose classes, like Tailwind CSS.

Example:

```html
<button class="px-4 py-2 rounded bg-blue-600 text-white">Save</button>
```

Interview answer: Utility-first CSS helps build consistent UIs quickly, but teams should manage readability and reuse carefully.

## 33. What Is CSS Architecture?

CSS architecture is the way styles are organized for scalability and maintainability.

Examples: BEM, utility-first CSS, CSS Modules, design tokens, component-scoped styles, SCSS partials.

## 34. How Do You Optimize CSS Performance?

Reduce unused CSS, avoid overly complex selectors, minimize layout thrashing, optimize animations, use transform/opacity for smooth motion, and avoid huge DOM/style recalculations.

## 35. Which CSS Properties Are Better For Animation Performance?

`transform` and `opacity` are usually better because they can often be handled by the compositor.

Avoid animating layout-heavy properties like `width`, `height`, `top`, and `left` when possible.

## 36. What Is Object-fit?

`object-fit` controls how replaced elements like images or videos fit their container.

Example:

```css
.avatar {
  width: 64px;
  height: 64px;
  object-fit: cover;
}
```

## 37. What Is clamp()?

`clamp()` creates a responsive value with minimum, preferred, and maximum limits.

Example:

```css
h1 {
  font-size: clamp(1.75rem, 3vw, 3rem);
}
```

## 38. What Are Container Queries?

Container queries apply styles based on a container's size rather than the viewport.

Example:

```css
.card-container {
  container-type: inline-size;
}

@container (min-width: 500px) {
  .card {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}
```

## 39. How Do You Convert Figma Designs To CSS?

Check layout, spacing, typography, colors, states, breakpoints, and reusable components. Then implement using design tokens, semantic HTML, responsive CSS, and accessible states.

Resume-based answer: In onboarding flows, I would map Figma sections to reusable React components and use CSS variables or Tailwind/MUI tokens for consistent spacing and colors.

## 40. How Do You Debug CSS?

Use browser DevTools to inspect computed styles, box model, layout overlays, responsive mode, accessibility panel, and performance tools.

Interview answer: I debug from the rendered element outward: inspect applied rules, overridden rules, computed values, layout model, and parent constraints.

## Detailed Practice Questions

## 41. Explain The CSS Box Model.

The CSS box model describes how every HTML element is rendered as a rectangular box. The box is made of four layers:

```text
content -> padding -> border -> margin
```

- `content` is the actual text, image, or child elements.
- `padding` is the space between the content and the border.
- `border` wraps the padding and content.
- `margin` is the space outside the border, separating the element from other elements.

Example:

```css
.card {
  width: 300px;
  padding: 20px;
  border: 2px solid #d0d7de;
  margin: 16px;
}
```

By default, `width: 300px` applies only to the content area. The actual visible width becomes `300px + 40px padding + 4px border`. With `box-sizing: border-box`, the padding and border are included inside the declared width, which makes layout calculations easier.

## 42. Explain Padding And Margin Shorthand.

Padding and margin shorthand let you set multiple sides in one declaration.

```css
.box {
  padding: 16px;
  margin: 10px 20px 30px 40px;
}
```

The shorthand values follow this pattern:

```text
1 value:  all sides
2 values: top/bottom, left/right
3 values: top, left/right, bottom
4 values: top, right, bottom, left
```

Example:

```css
.panel {
  padding: 12px 24px;
}
```

This means top and bottom padding are `12px`, while left and right padding are `24px`.

Interview answer: I use shorthand when the spacing pattern is clear, but I use longhand like `margin-top` or `padding-inline` when it improves readability or only one side needs to change.

## 43. Flexbox vs Grid?

Flexbox is mainly one-dimensional. It arranges items in a row or a column. Grid is two-dimensional. It controls rows and columns together.

Use Flexbox when the main problem is alignment or distribution along one axis.

```css
.actions {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 12px;
}
```

Use Grid when the layout needs rows and columns.

```css
.dashboard {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

Interview answer: I use Flexbox for navbars, button groups, toolbars, and aligning items inside a component. I use Grid for page layouts, dashboards, galleries, and layouts where both row and column structure matter.

## 44. Create A 60/40 Layout.

A 60/40 layout means one column takes 60% of the available width and the other takes 40%.

Using Grid:

```css
.layout {
  display: grid;
  grid-template-columns: 60% 40%;
  gap: 24px;
}
```

A more flexible version uses fractions:

```css
.layout {
  display: grid;
  grid-template-columns: 3fr 2fr;
  gap: 24px;
}
```

Responsive version:

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 24px;
}

@media (min-width: 768px) {
  .layout {
    grid-template-columns: 3fr 2fr;
  }
}
```

Interview answer: I prefer `3fr 2fr` because it represents the 60/40 relationship while allowing the browser to handle available space cleanly.

## 45. Center A Div Horizontally And Vertically.

The most common modern solution is Flexbox:

```css
.parent {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

`justify-content: center` centers along the main axis. `align-items: center` centers along the cross axis. In the default row direction, this means horizontal and vertical centering.

Grid can also be used:

```css
.parent {
  min-height: 100vh;
  display: grid;
  place-items: center;
}
```

Interview answer: I usually use Flexbox when I also need control over direction, gaps, or multiple child elements. I use Grid with `place-items: center` for simple single-element centering.

## 46. justify-content vs align-items.

In Flexbox, `justify-content` aligns items along the main axis, and `align-items` aligns items along the cross axis.

```css
.row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
```

For `flex-direction: row`:

```text
justify-content = horizontal alignment
align-items     = vertical alignment
```

For `flex-direction: column`, the axes switch:

```text
justify-content = vertical alignment
align-items     = horizontal alignment
```

Interview answer: I first check the flex direction. Then I decide whether I need to align along the main axis with `justify-content` or the cross axis with `align-items`.

## 47. Explain flex-grow, flex-shrink, And flex-basis.

These properties control how a flex item sizes itself inside a flex container.

- `flex-grow` controls how much an item can grow when extra space is available.
- `flex-shrink` controls how much an item can shrink when space is limited.
- `flex-basis` sets the starting size before growing or shrinking happens.

Example:

```css
.sidebar {
  flex: 0 0 260px;
}

.content {
  flex: 1 1 auto;
}
```

In this example, the sidebar starts at `260px` and does not grow or shrink. The content area can grow and shrink based on the available space.

The shorthand is:

```text
flex: grow shrink basis
```

Interview answer: I think of `flex-basis` as the initial size, `flex-grow` as how extra space is shared, and `flex-shrink` as how items compress when there is not enough room.

## 48. Explain position: relative vs absolute.

`position: relative` keeps the element in the normal document flow. If you apply `top`, `right`, `bottom`, or `left`, the element visually moves relative to where it would normally be.

```css
.badge {
  position: relative;
  top: -4px;
}
```

`position: absolute` removes the element from the normal document flow. It is positioned relative to the nearest ancestor that has a position other than `static`.

```css
.card {
  position: relative;
}

.card-badge {
  position: absolute;
  top: 12px;
  right: 12px;
}
```

Interview answer: I use `relative` when an element needs a small visual offset or when I want it to become the positioning context for an absolutely positioned child. I use `absolute` for overlays, badges, dropdown panels, and positioned decorative or UI elements.

## 49. Explain CSS Specificity.

Specificity decides which CSS selector wins when multiple selectors apply to the same element.

General priority:

```text
inline styles > IDs > classes/attributes/pseudo-classes > elements/pseudo-elements
```

Example:

```css
button {
  color: green;
}

.button {
  color: blue;
}

#submit {
  color: red;
}
```

If the element matches all three selectors, `#submit` wins because an ID has higher specificity than a class or element selector.

If specificity is equal, the rule that appears later in the CSS wins.

Interview answer: I avoid fighting specificity by using predictable class selectors, component-scoped styles, and consistent source order. I avoid unnecessary IDs and `!important` for regular styling.

## 50. display: none vs visibility: hidden.

`display: none` removes the element from the page layout. The element does not take up space.

```css
.modal {
  display: none;
}
```

`visibility: hidden` hides the element visually, but the element still occupies space in the layout.

```css
.placeholder {
  visibility: hidden;
}
```

Example difference:

```text
display: none       hidden and removed from layout
visibility: hidden  hidden but layout space remains
```

Interview answer: I use `display: none` when the element should not affect layout. I use `visibility: hidden` when I want to hide something but preserve its space.

## 51. block vs inline vs inline-block.

`block` elements start on a new line and usually take the full available width.

```css
.section {
  display: block;
}
```

`inline` elements stay within the text flow. Width and height do not apply in the normal way.

```css
.link {
  display: inline;
}
```

`inline-block` elements stay inline, but they can accept width, height, padding, and margin more predictably.

```css
.tag {
  display: inline-block;
  padding: 4px 8px;
}
```

Interview answer: I use block for sections and layout containers, inline for text-level elements, and inline-block for small UI pieces that should sit in text flow but still behave like boxes.

## 52. px vs % vs em vs rem vs vw/vh.

CSS units define how sizes are calculated.

- `px` is a fixed pixel value.
- `%` is relative to the parent or containing block.
- `em` is relative to the current element's font size.
- `rem` is relative to the root element's font size.
- `vw` is relative to viewport width.
- `vh` is relative to viewport height.

Reference diagram:

```text
%    -> percentage of a relevant containing value (property-dependent)
em   -> font size of this element; for font-size itself, the parent's font size
rem  -> root html font size
vw   -> 1% of viewport width
vh   -> 1% of viewport height
```

Example:

```css
.card {
  width: 80%;
  padding: 1rem;
  font-size: 1em;
  min-height: 50vh;
}
```

Assuming a root font size of `16px`, `2rem` equals `32px`. If a component has `font-size: 20px`, a child spacing value of `1.5em` equals `30px`. Viewport units are useful for fluid dimensions, but avoid using them without limits for body text; `clamp()` is usually safer. On mobile, newer `svh`, `lvh`, and `dvh` units can handle changing browser chrome more accurately than `vh`.

Interview answer: I use `rem` for consistent spacing and typography, `%` for fluid widths, `px` for borders or precise small values, and `vw`/`vh` for viewport-based sections. I use `em` when I want spacing to scale with the current component's font size.

## 53. How Do You Make A UI Responsive?

Responsive UI adapts well across screen sizes and devices.

Common techniques:

- Use fluid layouts with Flexbox and Grid.
- Start mobile-first, then enhance for larger screens.
- Use media queries for breakpoint-specific layout changes.
- Use relative units like `%`, `rem`, `fr`, `vw`, and `vh`.
- Make images flexible with `max-width: 100%`.
- Avoid fixed widths that break on small screens.
- Test with browser DevTools and real device sizes.

Example:

```css
.cards {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

img {
  max-width: 100%;
  height: auto;
}

@media (min-width: 768px) {
  .cards {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

Interview answer: I make UI responsive by combining mobile-first CSS, flexible layout systems, relative units, responsive images, and testing at multiple breakpoints.

## 54. Pseudo-class vs Pseudo-element.

A pseudo-class targets an element in a specific state or condition.

```css
button:hover {
  background: #2563eb;
}

input:focus {
  border-color: #2563eb;
}
```

Common pseudo-classes include `:hover`, `:focus`, `:checked`, `:disabled`, `:first-child`, and `:nth-child()`.

A pseudo-element targets a specific part of an element or creates a virtual element.

```css
.title::before {
  content: "";
  display: inline-block;
}

p::first-line {
  font-weight: 600;
}
```

Common pseudo-elements include `::before`, `::after`, `::placeholder`, `::first-line`, and `::selection`.

Interview answer: Pseudo-classes style states. Pseudo-elements style parts of elements or generated content.

## 55. Given HTML, Write A Selector To Target A Particular Element.

When writing a selector, first identify the most stable and specific hook available: a class, attribute, parent context, or semantic structure. Avoid overly broad selectors and avoid IDs unless the ID is intentionally unique and stable.

Example HTML:

```html
<section class="profile-card">
  <h2 class="profile-card__title">User Profile</h2>
  <button class="button button--primary" data-action="save">Save</button>
</section>
```

Target the save button by class and attribute:

```css
.profile-card .button[data-action="save"] {
  background: #2563eb;
}
```

Target only the title inside the profile card:

```css
.profile-card > .profile-card__title {
  margin-bottom: 12px;
}
```

Interview answer: I choose selectors that are specific enough to target the intended element, but not so specific that they become fragile. I prefer class and attribute selectors for UI components because they are reusable and readable.

## 56. How Do You Center Multiple span Elements?

`span` elements are inline by default. Inline elements behave like text, so multiple spans can be centered by applying `text-align: center` to their parent container.

Example HTML:

```html
<div class="tags">
  <span>HTML</span>
  <span>CSS</span>
  <span>JavaScript</span>
</div>
```

Simple solution:

```css
.tags {
  text-align: center;
}

.tags span {
  display: inline-block;
  padding: 6px 12px;
  margin: 4px;
  border: 1px solid #d1d5db;
}
```

Why this works:

```text
span is inline by default
inline elements are affected by text-align
text-align: center on the parent centers the spans as inline content
```

The `display: inline-block` on each span is optional for centering, but useful because it allows padding, margin, width, and height to behave more like a small UI box.

Flexbox solution:

```css
.tags {
  display: flex;
  justify-content: center;
  gap: 8px;
  flex-wrap: wrap;
}
```

Why Flexbox is useful:

```text
justify-content: center = centers the spans horizontally
gap: 8px                = adds consistent spacing
flex-wrap: wrap         = allows spans to move to the next line on small screens
```

Interview answer: If I have multiple span elements and want to center them as a group, I can wrap them in a parent and use `text-align: center` because spans are inline by default. For better control over spacing, wrapping, and alignment, I would use Flexbox with `justify-content: center`, `gap`, and `flex-wrap: wrap`.

## 57. Do width And height Work On Inline Elements?

For normal inline elements like `<span>` and `<a>`, `width` and `height` do not work like they do on block elements.

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

Even though `width` and `height` are written, the span still sizes mainly based on its text content.

```text
Status: [Approved]
```

Not like this:

```text
Status: [Approved                         ]
```

Important points:

```text
width  = ignored for normal inline elements
height = ignored for normal inline elements
```

But inline elements can still visually change because of:

- longer text content
- `font-size`
- `line-height`
- horizontal padding

Example:

```css
.status-text {
  padding-left: 12px;
  padding-right: 12px;
  background: #dcfce7;
}
```

This can make the inline element look wider:

```text
Status: [   Approved   ]
```

If you want `width`, `height`, padding, and margin to behave predictably, use `inline-block`.

```css
.status-text {
  display: inline-block;
  width: 120px;
  height: 36px;
  padding: 8px 12px;
}
```

Interview answer: Normal inline elements size themselves based on their content, so `width` and `height` do not apply normally. If I need an inline element to accept width, height, padding, and margin like a box, I use `display: inline-block`.

## 58. What Is CSS Inheritance?

Inheritance is the process by which some computed CSS property values pass from a parent element to its descendants. Text-related properties such as `color`, `font-family`, and `line-height` commonly inherit. Layout and box-model properties such as `margin`, `padding`, `border`, `width`, and `display` normally do not.

```html
<section class="verification-panel">
  <h2>Identity verification</h2>
  <p>The application is under review.</p>
</section>
```

```css
.verification-panel {
  color: #1f2937;
  font-family: Arial, sans-serif;
  border: 1px solid #cbd5e1;
}
```

```text
verification-panel
|-- h2 -> inherits color and font-family; does not inherit border
`-- p  -> inherits color and font-family; does not inherit border
```

Inheritance is different from the cascade. The cascade first finds a winning declared value for an element. If no declaration wins and the property is inheritable, the element may receive its parent's computed value.

The global keywords give explicit control:

- `inherit`: take the computed value from the parent, even for a normally non-inherited property.
- `initial`: use the property's specification-defined initial value.
- `unset`: behave as `inherit` for inherited properties and `initial` for other properties.
- `revert`: roll back to the value from an earlier cascade origin, commonly browser or user styles.

```css
button {
  font: inherit;
  color: inherit;
}
```

Interview answer: Inheritance lets descendants reuse certain parent values, especially typography and color. It is not the same as specificity: specificity chooses between competing declarations, while inheritance supplies a value when the child has no winning declaration for an inherited property.

## Final Cheat Sheet

```text
Selectors: class for reuse, ID for unique targets
Specificity: inline > id > class > element
Inheritance: typography often inherits; layout and box properties usually do not
Box model: content + padding + border + margin
Layout: Flexbox for one dimension, Grid for two
Responsive: mobile-first, media queries, relative units
Accessibility: focus-visible, contrast, readable text
Animations: prefer transform and opacity
Architecture: tokens, utilities, components, avoid global mess
```
