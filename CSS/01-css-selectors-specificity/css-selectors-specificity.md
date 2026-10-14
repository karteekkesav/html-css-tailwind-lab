# CSS Selectors And Specificity

## What It Means

Selectors target HTML elements. Specificity decides which rule wins when multiple rules apply.

## Common Selectors

```css
button {}
.button {}
#save-button {}
[data-state="active"] {}
.card:hover {}
```

## Specificity Diagram

```text
inline style      highest
ID selector
class/attribute/pseudo-class
element/pseudo-element
source order      tie breaker
```

## Examples With Explanation

### 1. Element Selector

```html
<button>Save</button>
```

```css
button {
  color: green;
}
```

This targets every `<button>` element on the page. Element selectors have low specificity, so they are useful for base styles.

Interview explanation: Element selectors are good for setting default styles, but I avoid relying on them for component-specific styling because they can affect too many elements.

### 2. Class Selector

```html
<button class="primary-button">Save</button>
```

```css
.primary-button {
  color: blue;
}
```

This targets any element with the class `primary-button`. Class selectors are reusable and have higher specificity than element selectors.

Interview explanation: I prefer classes for styling because they are reusable, readable, and easier to maintain than IDs.

### 3. ID Selector

```html
<button id="save-button">Save</button>
```

```css
#save-button {
  color: red;
}
```

This targets the element with the ID `save-button`. IDs should be unique on a page and have high specificity.

Interview explanation: IDs are powerful, but I avoid using them for regular styling because they make CSS harder to override.

### 4. Attribute Selector

```html
<button data-state="active">Save</button>
```

`data-state="active"` is a custom HTML data attribute.

Breakdown:

```text
data-state = attribute name
active     = attribute value
```

HTML allows custom attributes that start with `data-`. They are commonly used to store extra information about an element, especially UI state.

For example, a button can be active, inactive, loading, selected, expanded, or disabled:

```html
<button data-state="active">Save</button>
<button data-state="inactive">Cancel</button>
<button data-state="loading">Submitting...</button>
```

The browser does not automatically give `data-state` any visual meaning. It is just information in the HTML. CSS or JavaScript can read that information and use it.

```css
[data-state="active"] {
  border-color: #2563eb;
}
```

This CSS selector means:

```text
Select any element that has data-state="active".
```

So this rule applies to the button below:

```html
<button data-state="active">Save</button>
```

But it does not apply to this button:

```html
<button data-state="inactive">Cancel</button>
```

If multiple elements have the same matching attribute and value, all of them will receive the same CSS style.

Example:

```html
<button data-state="active">Profile</button>
<button data-state="active">Settings</button>
<button data-state="inactive">Billing</button>
```

```css
[data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
}
```

In this example, `Profile` and `Settings` become blue because both have `data-state="active"`. `Billing` does not become blue because it has `data-state="inactive"`.

If you only want active buttons inside a specific component to become blue, make the selector more specific by adding a parent class:

```html
<nav class="tabs">
  <button data-state="active">Profile</button>
  <button data-state="inactive">Billing</button>
</nav>

<div class="filter-list">
  <button data-state="active">Open</button>
</div>
```

```css
.tabs [data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
}
```

Now only active elements inside `.tabs` become blue. The active button inside `.filter-list` is not affected by this rule.

Attribute selectors have the same specificity level as classes.

Interview explanation: Attribute selectors are useful for styling UI states, test-friendly markup, and data-driven components.

## Can We Change data-state Conditionally?

Yes. `data-state="active"` and `data-state="inactive"` can be changed conditionally.

Common tab requirement:

```text
selected tab   = active
other tabs     = inactive
```

CSS does not decide which tab is active by itself. CSS only styles whatever state is present in the HTML.

The active state is usually controlled by:

```text
JavaScript
React state
Angular/Vue state
server-rendered HTML
```

## Static HTML Example

```html
<nav class="tabs">
  <button data-state="active">Profile</button>
  <button data-state="inactive">Settings</button>
  <button data-state="inactive">Billing</button>
</nav>
```

```css
.tabs button {
  color: #374151;
  border: 1px solid #d1d5db;
  background: white;
}

.tabs button[data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
  background: #eff6ff;
}
```

Visual:

```text
[ Profile active ] [ Settings inactive ] [ Billing inactive ]
```

Only `Profile` gets the active style because only `Profile` has:

```html
data-state="active"
```

If the user selects `Settings`, the HTML should become:

```html
<nav class="tabs">
  <button data-state="inactive">Profile</button>
  <button data-state="active">Settings</button>
  <button data-state="inactive">Billing</button>
</nav>
```

Now `Settings` gets the active style.

## JavaScript Example

HTML:

```html
<nav class="tabs">
  <button data-state="active">Profile</button>
  <button data-state="inactive">Settings</button>
  <button data-state="inactive">Billing</button>
</nav>
```

CSS:

```css
.tabs button {
  color: #374151;
  border: 1px solid #d1d5db;
  background: white;
}

.tabs button[data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
  background: #eff6ff;
}
```

JavaScript:

```js
const tabButtons = document.querySelectorAll(".tabs button");

tabButtons.forEach((button) => {
  button.addEventListener("click", () => {
    tabButtons.forEach((tab) => {
      tab.dataset.state = "inactive";
    });

    button.dataset.state = "active";
  });
});
```

Explanation:

```text
1. User clicks a tab.
2. JavaScript makes all tabs inactive.
3. JavaScript makes the clicked tab active.
4. CSS automatically applies active styles to the active tab.
```

Important:

```text
CSS styles the state.
JavaScript changes the state.
```

## React Example

In React, this is usually done with component state.

```jsx
import { useState } from "react";

const tabs = ["Profile", "Settings", "Billing"];

function AccountTabs() {
  const [activeTab, setActiveTab] = useState("Profile");

  return (
    <nav className="tabs">
      {tabs.map((tab) => (
        <button
          key={tab}
          data-state={activeTab === tab ? "active" : "inactive"}
          onClick={() => setActiveTab(tab)}
        >
          {tab}
        </button>
      ))}
    </nav>
  );
}
```

CSS:

```css
.tabs button {
  color: #374151;
  border: 1px solid #d1d5db;
  background: white;
}

.tabs button[data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
  background: #eff6ff;
}
```

How it works:

```text
activeTab stores the selected tab.
If activeTab === tab, data-state becomes active.
Otherwise, data-state becomes inactive.
When user clicks a tab, setActiveTab(tab) updates the selected tab.
React re-renders the buttons with updated data-state values.
CSS applies the correct styles.
```

Example flow:

```text
initial activeTab = "Profile"
Profile button  = data-state active
Settings button = data-state inactive
Billing button  = data-state inactive

user clicks Settings
activeTab = "Settings"
Profile button  = data-state inactive
Settings button = data-state active
Billing button  = data-state inactive
```

## Should We Use class Or data-state?

Both are valid.

Class approach:

```jsx
<button className={activeTab === tab ? "tab active" : "tab"}>
  {tab}
</button>
```

```css
.tab.active {
  color: #2563eb;
}
```

Attribute approach:

```jsx
<button data-state={activeTab === tab ? "active" : "inactive"}>
  {tab}
</button>
```

```css
.tabs button[data-state="active"] {
  color: #2563eb;
}
```

Interview explanation: I use a class like `.active` for simple styling. I use `data-state` when the component has clear UI states such as active, inactive, loading, open, closed, selected, or disabled. This is common in component libraries.

Best interview answer: Yes, the button state can be changed conditionally. CSS only styles `[data-state="active"]`; JavaScript or React decides which button receives `data-state="active"`. In React, I store the selected tab in state and set `data-state={activeTab === tab ? "active" : "inactive"}` for each button.

## Class Selectors vs Attribute Selectors

Class selectors and attribute selectors can target the same element. This is not automatically a problem. A conflict happens only when both selectors try to set the same CSS property.

### Scenario 1. No Conflict

```html
<button class="primary-button" data-state="active">Save</button>
```

```css
.primary-button {
  background-color: #2563eb;
}

[data-state="active"] {
  border-color: #2563eb;
}
```

There is no conflict here because each rule changes a different property.

Result:

```text
background-color comes from .primary-button
border-color comes from [data-state="active"]
```

Interview explanation: Multiple selectors can style the same element safely when they control different CSS properties.

### Scenario 2. Conflict With Equal Specificity

```html
<button class="primary-button" data-state="active">Save</button>
```

```css
.primary-button {
  color: white;
}

[data-state="active"] {
  color: blue;
}
```

Both selectors target the same element and both set `color`.

Class selectors and attribute selectors have the same specificity level:

```text
.primary-button       = class selector
[data-state="active"] = attribute selector
```

Because specificity is equal, source order decides the winner. The later rule wins, so the text becomes blue.

If the order is reversed:

```css
[data-state="active"] {
  color: blue;
}

.primary-button {
  color: white;
}
```

Now the text becomes white because `.primary-button` appears later.

Interview explanation: When class and attribute selectors set the same property and have equal specificity, the rule written later in the CSS wins.

### Scenario 3. Combined Selector Wins

```html
<button class="primary-button" data-state="active">Save</button>
```

```css
.primary-button {
  color: white;
}

.primary-button[data-state="active"] {
  color: blue;
}
```

The text becomes blue.

Why:

```text
.primary-button                 = one class-level selector
.primary-button[data-state="active"] = class + attribute selector
```

The second selector is more specific because it combines a class selector and an attribute selector.

Interview explanation: Combining a class and an attribute is useful when you want to style a particular state of a particular component.

### Scenario 4. Attribute State Overrides Base Class

This is a common real-world pattern.

```html
<button class="button" data-state="active">Profile</button>
<button class="button" data-state="inactive">Billing</button>
```

```css
.button {
  color: #374151;
  border-color: #d1d5db;
}

.button[data-state="active"] {
  color: #2563eb;
  border-color: #2563eb;
}
```

Here `.button` provides the default style. `.button[data-state="active"]` overrides only active buttons.

Result:

```text
Profile = active blue style
Billing = default gray style
```

Interview explanation: I often use a class for the base component style and an attribute for the component state.

### Scenario 5. Parent Scope Avoids Unwanted Styling

```html
<nav class="tabs">
  <button class="button" data-state="active">Profile</button>
</nav>

<section class="modal">
  <button class="button" data-state="active">Confirm</button>
</section>
```

```css
.tabs .button[data-state="active"] {
  color: #2563eb;
}
```

Only the active button inside `.tabs` becomes blue. The active button inside `.modal` is not affected.

Interview explanation: When many components use the same state attribute, I scope the selector with a parent class to avoid styling unrelated elements.

### Scenario 6. ID Still Beats Both

```html
<button id="save-button" class="primary-button" data-state="active">Save</button>
```

```css
.primary-button[data-state="active"] {
  color: blue;
}

#save-button {
  color: red;
}
```

The text becomes red because an ID selector has higher specificity than class and attribute selectors.

Interview explanation: This is why I avoid ID selectors for normal component styling. They can easily override reusable class and state styles.

### Best Practice

Use classes for base component styles:

```css
.button {
  padding: 8px 16px;
  border: 1px solid #d1d5db;
}
```

Use attributes for state:

```css
.button[data-state="active"] {
  border-color: #2563eb;
}
```

This keeps the CSS clear:

```text
class     = what the element is
attribute = what state the element is in
```

Strong interview answer: Class selectors and attribute selectors do not conflict by default. A conflict happens only when both set the same property on the same element. Since classes and attributes have equal specificity, source order decides unless one selector is more specific, such as `.button[data-state="active"]`.

### 5. Pseudo-class Selector

```css
.primary-button:hover {
  background-color: #1d4ed8;
}
```

`:hover` is a pseudo-class. A pseudo-class styles an element when it is in a specific state or condition.

Pseudo-classes start with one colon:

```text
:hover
:focus
:checked
:disabled
:first-child
:nth-child()
```

Pseudo-classes have the same specificity level as class selectors.

## Pseudo-class Examples With Explanation

### 1. :hover

```html
<button class="primary-button">Save</button>
```

```css
.primary-button {
  background-color: #2563eb;
  color: white;
}

.primary-button:hover {
  background-color: #1d4ed8;
}
```

`:hover` applies when the user places the mouse pointer over the button.

Result:

```text
Normal button color = #2563eb
Hover button color  = #1d4ed8
```

Interview explanation: `:hover` is commonly used for interactive feedback on buttons, links, cards, and menu items.

### 2. :focus

```html
<input class="form-input" type="text" placeholder="Enter name">
```

```css
.form-input {
  border: 1px solid #d1d5db;
}

.form-input:focus {
  border-color: #2563eb;
  outline: 2px solid #bfdbfe;
}
```

`:focus` applies when the input is selected, usually by clicking it or reaching it with the keyboard.

Interview explanation: `:focus` is important for accessibility because keyboard users need a clear visual indicator of the currently active element.

## Difference Between outline And border

`border` is part of the CSS box model. It sits around the padding and content, and it can affect the element's size or layout.

```css
.form-input {
  border: 2px solid #d1d5db;
}
```

If the element uses the default `box-sizing: content-box`, adding a border increases the total visible size of the element.

```text
total width = content width + padding + border
```

`outline` is drawn outside the element. It is not part of the box model, so it does not take up layout space and does not move nearby elements.

```css
.form-input:focus {
  outline: 3px solid #2563eb;
  outline-offset: 2px;
}
```

`outline-offset` controls the gap between the element and the outline.

### Example

```html
<input class="form-input" type="text" placeholder="Enter name">
```

```css
.form-input {
  padding: 10px 12px;
  border: 1px solid #d1d5db;
}

.form-input:focus {
  border-color: #2563eb;
  outline: 3px solid #bfdbfe;
  outline-offset: 2px;
}
```

In this example:

```text
border  = normal input boundary
outline = extra focus indicator outside the input
```

The border is part of the input's design. The outline appears only when the input is focused and helps users see which field is active.

### Key Differences

```text
border:
- part of the box model
- can affect width and height
- commonly used for normal element design
- each side can be styled separately

outline:
- not part of the box model
- does not affect layout
- commonly used for focus/accessibility states
- drawn around the whole element
```

Interview answer: A border is part of the element's box model and can affect layout. An outline is drawn outside the element and does not affect layout, so it is commonly used for accessible focus states.

### 3. :checked

```html
<input class="terms-checkbox" type="checkbox" checked>
<label>I agree to the terms</label>
```

```css
.terms-checkbox:checked {
  accent-color: #2563eb;
}
```

`:checked` applies when a checkbox or radio button is selected.

Interview explanation: `:checked` is useful for styling selected checkboxes, selected radio buttons, toggles, and custom form controls.

### 4. :disabled

```html
<button class="submit-button" disabled>Submit</button>
```

```css
.submit-button {
  background-color: #2563eb;
  color: white;
}

.submit-button:disabled {
  background-color: #9ca3af;
  cursor: not-allowed;
}
```

`:disabled` applies when a form control is disabled.

Result:

```text
Enabled button  = blue
Disabled button = gray
```

Interview explanation: `:disabled` helps communicate that a button or input cannot currently be used.

### 5. :first-child

```html
<ul class="menu">
  <li>Dashboard</li>
  <li>Reports</li>
  <li>Settings</li>
</ul>
```

```css
.menu li:first-child {
  font-weight: 700;
}
```

`:first-child` applies to an element only if it is the first child of its parent.

In this example, only `Dashboard` becomes bold.

Interview explanation: `:first-child` is useful when the first item in a list or group needs special styling.

### 6. :nth-child()

```html
<table class="users-table">
  <tr><td>Aarav</td></tr>
  <tr><td>Diya</td></tr>
  <tr><td>Kabir</td></tr>
  <tr><td>Meera</td></tr>
</table>
```

```css
.users-table tr:nth-child(even) {
  background-color: #f3f4f6;
}
```

`:nth-child(even)` applies to every even row.

Result:

```text
Row 1 = normal
Row 2 = gray background
Row 3 = normal
Row 4 = gray background
```

Interview explanation: `:nth-child()` is useful for zebra-striped tables, grids, lists, and selecting elements based on their position.

### 7. Multiple Pseudo-classes Together

```html
<button class="primary-button">Save</button>
<button class="primary-button" disabled>Submit</button>
```

```css
.primary-button:hover {
  background-color: #1d4ed8;
}

.primary-button:disabled {
  background-color: #9ca3af;
  cursor: not-allowed;
}
```

If the button is disabled, the disabled style should communicate that it is not interactive. In real projects, you may also prevent hover styling on disabled buttons:

```css
.primary-button:not(:disabled):hover {
  background-color: #1d4ed8;
}
```

This means:

```text
Apply hover style only when the button is not disabled.
```

Important: `:not(:disabled)` does not mean "only elements that were disabled before and later became enabled."

It means:

```text
Select elements that are currently not disabled.
```

So the selector is checked based on the element's current state in the browser.

Breakdown:

```css
.primary-button:not(:disabled):hover {
  background-color: #1d4ed8;
}
```

```text
.primary-button = select elements with class primary-button
:not(:disabled) = only if they are not disabled right now
:hover          = only when the user hovers over them
```

Example:

```html
<button class="primary-button">Save</button>
<button class="primary-button" disabled>Submit</button>
<button class="primary-button">Cancel</button>
```

```css
.primary-button:not(:disabled):hover {
  background-color: #1d4ed8;
}
```

Result:

```text
Save   = gets hover style because it is not disabled
Submit = does not get hover style because it is disabled
Cancel = gets hover style because it is not disabled
```

If JavaScript later removes the `disabled` attribute from `Submit`, then `Submit` can also match the selector.

```html
<button class="primary-button">Submit</button>
```

Now `Submit` is not disabled, so when the user hovers over it, the hover style applies.

Interview explanation: `:not(:disabled)` matches any element that is currently enabled. It is not about the element's past state. CSS does not remember whether an element was disabled before. It only checks the current HTML/browser state.

Interview explanation: I often combine pseudo-classes to make states more accurate, such as `:not(:disabled):hover`.

### Best Interview Answer

Pseudo-classes style elements based on state or condition. Examples include `:hover` for mouse interaction, `:focus` for active form fields, `:checked` for selected inputs, `:disabled` for unavailable controls, and `:nth-child()` for position-based styling. They have the same specificity level as class selectors.

Interview explanation: Pseudo-classes are used for states like hover, focus, checked, disabled, and first-child.

### 6. Pseudo-element Selector

```css
.card::before {
  content: "";
  display: block;
  height: 4px;
  background: #2563eb;
}
```

`::before` creates a virtual element before the content of `.card`. This virtual element does not need to exist in the HTML.

Pseudo-elements start with two colons:

```text
::before
::after
::placeholder
::first-line
::first-letter
::selection
```

Pseudo-elements have low specificity, similar to element selectors.

## Pseudo-element Examples With Explanation

### 1. ::before

```html
<div class="card">
  <h3>Account Details</h3>
  <p>Update your profile information.</p>
</div>
```

```css
.card::before {
  content: "";
  display: block;
  height: 4px;
  background: #2563eb;
}
```

This adds a visual strip before the card's actual content.

The browser behaves as if something like this exists visually:

```html
<div class="card">
  <!-- ::before appears here visually -->
  <h3>Account Details</h3>
  <p>Update your profile information.</p>
</div>
```

Important: `::before` will not appear unless the `content` property is defined.

```css
.card::before {
  content: "";
}
```

Even if the content is empty, `content: ""` tells the browser to create the pseudo-element.

Interview explanation: `::before` is useful for adding decorative elements, icons, labels, or visual markers without adding extra HTML.

### 2. ::after

```html
<a class="external-link" href="https://example.com">Documentation</a>
```

```css
.external-link::after {
  content: " external";
  font-size: 12px;
  color: #6b7280;
}
```

This adds text after the link content.

Visual result:

```text
Documentation external
```

Another common use is adding a required-field symbol:

```html
<label class="required-label">Email</label>
```

```css
.required-label::after {
  content: " *";
  color: #dc2626;
}
```

Visual result:

```text
Email *
```

Interview explanation: `::after` is used to add generated content after an element's real content. It is common for badges, required stars, link indicators, and decorative UI.

## What Is content In CSS?

`content` is a CSS property used mainly with `::before` and `::after`.

It tells the browser what generated content should be placed before or after an element's real content.

Example:

```html
<p class="message">Payment successful</p>
```

```css
.message::before {
  content: "Success: ";
  color: #15803d;
  font-weight: 700;
}
```

Visual result:

```text
Success: Payment successful
```

Important: the text `Success:` is not actually written in the HTML. It is generated by CSS.

For `::before` and `::after`, `content` is required. Without it, the pseudo-element will usually not appear.

```css
.card::before {
  content: "";
  display: block;
  height: 4px;
  background: #2563eb;
}
```

Here `content: ""` means "create an empty pseudo-element." Even though it has no text, it can still be styled as a visual line, dot, badge, or shape.

## Where content Is Helpful

### 1. Required Field Star

```html
<label class="required-label">Email</label>
```

```css
.required-label::after {
  content: " *";
  color: #dc2626;
}
```

Visual result:

```text
Email *
```

This is useful when many form labels need the same required indicator.

Interview note: For accessibility, do not rely only on this visual star. The form should still communicate required fields through HTML, text, or ARIA where needed.

### 2. External Link Indicator

```html
<a class="external-link" href="https://example.com">Documentation</a>
```

```css
.external-link::after {
  content: " ↗";
  font-size: 12px;
}
```

Visual result:

```text
Documentation ↗
```

This helps users understand that the link opens or points outside the current site.

### 3. Status Label

```html
<span class="status" data-status="new">Invoice</span>
```

```css
.status[data-status="new"]::after {
  content: " New";
  color: #2563eb;
  font-size: 12px;
  font-weight: 700;
}
```

Visual result:

```text
Invoice New
```

This is helpful for badges, labels, and small UI indicators.

### 4. Decorative Line Or Accent

```html
<div class="card">
  <h3>Account Details</h3>
</div>
```

```css
.card::before {
  content: "";
  display: block;
  width: 48px;
  height: 4px;
  background-color: #2563eb;
  margin-bottom: 12px;
}
```

Here `content: ""` creates an empty pseudo-element, and the CSS styles it as a small line above the card title.

This is useful for decoration without adding extra empty `<div>` elements in HTML.

### 5. Quotes Around Text

```html
<blockquote class="quote">CSS is powerful when selectors stay simple.</blockquote>
```

```css
.quote::before {
  content: "\"";
}

.quote::after {
  content: "\"";
}
```

Visual result:

```text
"CSS is powerful when selectors stay simple."
```

This shows how `content` can insert text before and after real content.

### 6. Number Or Prefix

```html
<p class="tip">Use class selectors for reusable styles.</p>
```

```css
.tip::before {
  content: "Tip: ";
  font-weight: 700;
  color: #2563eb;
}
```

Visual result:

```text
Tip: Use class selectors for reusable styles.
```

This is useful for repeated UI patterns like notes, warnings, tips, or helper text.

## Best Interview Answer

`content` is used with pseudo-elements like `::before` and `::after` to insert generated content through CSS. It can insert text, symbols, empty visual elements, badges, required stars, or decorative shapes. If `::before` or `::after` does not have `content`, it usually will not render.

### 3. ::placeholder

```html
<input class="form-input" type="email" placeholder="Enter email">
```

```css
.form-input::placeholder {
  color: #9ca3af;
  font-style: italic;
}
```

`::placeholder` styles the placeholder text inside an input or textarea.

Only the placeholder is affected. The user's typed text is not affected by this selector.

```css
.form-input {
  color: #111827;
}

.form-input::placeholder {
  color: #9ca3af;
}
```

Result:

```text
typed text        = dark
placeholder text  = gray
```

Interview explanation: `::placeholder` targets only placeholder text, not the actual input value.

### 4. ::first-line

```html
<p class="intro">
  CSS selectors help us target elements and apply styles based on structure,
  state, attributes, and relationships.
</p>
```

```css
.intro::first-line {
  font-weight: 700;
  color: #2563eb;
}
```

`::first-line` styles only the first rendered line of text.

Important: the first line can change depending on screen size, font size, and container width.

Interview explanation: `::first-line` is useful for article-style text effects, but it depends on how the browser wraps text.

### 5. ::first-letter

```html
<p class="article-text">
  selectors are one of the most important parts of CSS.
</p>
```

```css
.article-text::first-letter {
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
}
```

`::first-letter` styles only the first letter of the text.

Interview explanation: `::first-letter` is mostly used for editorial designs, such as drop caps in articles.

### 6. ::selection

```css
::selection {
  background: #2563eb;
  color: white;
}
```

`::selection` styles text when the user selects it with the mouse or keyboard.

Interview explanation: `::selection` can customize selected text styling, but it should still maintain readable contrast.

## Pseudo-element vs Pseudo-class

Pseudo-class means state or condition.

```css
button:hover {
  background: #1d4ed8;
}
```

This means the button is styled when it is hovered.

Pseudo-element means a specific part of an element or generated content.

```css
button::after {
  content: ">";
}
```

This means extra generated content is added after the button's text.

Simple difference:

```text
pseudo-class   = state of an element
pseudo-element = part of an element or generated content
```

## Common Interview Question

Question: Why is my `::before` not visible?

```css
.card::before {
  display: block;
  height: 4px;
  background: #2563eb;
}
```

Answer: The `content` property is missing. For `::before` and `::after`, the pseudo-element is created only when `content` is set.

Correct version:

```css
.card::before {
  content: "";
  display: block;
  height: 4px;
  background: #2563eb;
}
```

Interview explanation: Pseudo-elements are useful for styling parts of elements or adding decorative content without extra HTML.

## Specificity Winner Example

```html
<button id="save-button" class="primary-button">Save</button>
```

```css
button {
  color: green;
}

.primary-button {
  color: blue;
}

#save-button {
  color: red;
}
```

The button text becomes red.

Why:

```text
button          element selector = low specificity
.primary-button class selector   = medium specificity
#save-button    ID selector      = high specificity
```

The ID selector wins because it has higher specificity than the class selector and element selector.

## Source Order Example

```html
<button class="primary-button">Save</button>
```

```css
.primary-button {
  color: blue;
}

.primary-button {
  color: purple;
}
```

The button text becomes purple because both selectors have equal specificity. When specificity is the same, the later rule wins.

Interview explanation: Source order only decides the winner when specificity is equal.

## Combined Selector Example

```html
<div class="card">
  <button class="primary-button">Save</button>
</div>
```

```css
.primary-button {
  color: blue;
}

.card .primary-button {
  color: orange;
}
```

The button text becomes orange.

Why:

```text
.primary-button       = one class
.card .primary-button = two classes
```

The second selector is more specific because it contains two class selectors.

Interview explanation: Combining selectors increases specificity, but I avoid making selectors too deeply nested because they become hard to override.

## !important Example

```css
.primary-button {
  color: blue !important;
}

#save-button {
  color: red;
}
```

Even though `#save-button` has higher normal specificity, the blue color wins because `!important` overrides normal declarations.

Normally, an ID selector beats a class selector:

```css
.primary-button {
  color: blue;
}

#save-button {
  color: red;
}
```

Result:

```text
red wins because ID specificity is higher
```

But when the class declaration uses `!important`, it becomes more powerful than a normal ID declaration:

```css
.primary-button {
  color: blue !important;
}

#save-button {
  color: red;
}
```

Result:

```text
blue wins because !important beats normal CSS declarations
```

### If Both Rules Use !important

If both declarations are marked `!important`, then specificity is checked again.

```css
.primary-button {
  color: blue !important;
}

#save-button {
  color: red !important;
}
```

Result:

```text
red wins because both are !important, and the ID selector has higher specificity
```

### If Specificity Is Equal

If both rules use `!important` and have the same specificity, source order decides.

```css
.primary-button {
  color: blue !important;
}

.primary-button {
  color: purple !important;
}
```

Result:

```text
purple wins because both rules have equal specificity and the purple rule appears later
```

### Inline Style vs !important

Inline styles are normally stronger than regular CSS.

```html
<button class="primary-button" style="color: red;">Save</button>
```

```css
.primary-button {
  color: blue;
}
```

Result:

```text
red wins because inline style is stronger than a normal class rule
```

But an external CSS rule with `!important` can override a normal inline style:

```html
<button class="primary-button" style="color: red;">Save</button>
```

```css
.primary-button {
  color: blue !important;
}
```

Result:

```text
blue wins because !important overrides the normal inline color declaration
```

### Real Use Case

Sometimes a third-party library applies styles that are hard to override.

```css
.library-button {
  color: red;
}
```

You may temporarily override it:

```css
.primary-button {
  color: blue !important;
}
```

But a better long-term solution is usually to make the selector more intentional or use the library's theming/customization system.

```css
.app-theme .primary-button {
  color: blue;
}
```

### Why Overusing !important Is Bad

If many rules use `!important`, the CSS becomes harder to debug.

```css
.button {
  color: blue !important;
}

.button.danger {
  color: red !important;
}

.modal .button {
  color: green !important;
}
```

Now it is harder to quickly understand which rule wins, because everything is trying to force priority.

Interview explanation: I treat `!important` as a last option. It can be useful for utility overrides or third-party CSS conflicts, but overusing it makes styles unpredictable.

## Practical Interview Scenario

Question: Why is my button not turning blue?

```html
<button id="save-button" class="primary-button">Save</button>
```

```css
#save-button {
  color: red;
}

.primary-button {
  color: blue;
}
```

Answer: The ID selector has higher specificity than the class selector, so the button remains red. To fix it, avoid the ID selector for styling, or write a more intentional class-based rule.

Better approach:

```css
.primary-button {
  color: blue;
}

.primary-button.is-danger {
  color: red;
}
```

This approach keeps the styling reusable and easier to override.

## Resume-Based Example

For a React onboarding module, prefer reusable classes or component-scoped styles over ID-heavy CSS. This keeps Proof of Identity, Proof of Address, and Account Type screens consistent.

## Interview Answer

Specificity is how browsers decide which CSS rule applies. I keep selectors simple, avoid unnecessary IDs, and rely on reusable classes, utilities, or component styles.

## Common Mistakes

- Overusing `!important`.
- Styling everything with IDs.
- Writing deeply nested selectors.
- Depending on source order accidentally.
