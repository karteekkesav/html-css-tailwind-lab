# HTML Interview Questions And Answers

This file is the master revision guide for HTML interview preparation. Focus first on the high-priority questions, then revise the additional questions.

## Quick Priority Map

```text
HTML Interview Core
|
+-- Structure: doctype, html, head, body, semantic tags
+-- Accessibility: labels, headings, alt, ARIA, WCAG
+-- Forms: input types, validation, fieldset, error messages
+-- Browser APIs: storage, cookies, HTML5 APIs
+-- Performance: async, defer, images, preload
+-- SEO: metadata, headings, semantic HTML, links
```

## 1. What Is Semantic HTML?

Semantic HTML means using elements that describe the meaning and purpose of content.

Examples: `header`, `nav`, `main`, `section`, `article`, `aside`, and `footer`.

Interview answer: Semantic HTML improves accessibility, SEO, maintainability, and readability. In React applications, it also helps create cleaner component structures without unnecessary `div` wrappers.

| Element | Purpose |
| --- | --- |
| `header` | Introductory content for a page or section, often containing a heading, logo, or tools |
| `nav` | A major group of navigation links |
| `main` | The unique primary content of the page; normally use one visible `main` per page |
| `section` | A thematic group of related content, usually with a heading |
| `article` | Self-contained content that could stand alone or be reused independently |
| `aside` | Supporting or complementary content, such as help or related links |
| `footer` | Closing information for a page or section, such as copyright or author details |

Example:

```html
<header>
  <h1>Digital Onboarding Portal</h1>
  <nav aria-label="Primary navigation">
    <a href="#identity">Identity</a>
    <a href="#address">Address</a>
  </nav>
</header>

<main>
  <section aria-labelledby="identity-heading">
    <h2 id="identity-heading">Proof Of Identity</h2>
    <p>Upload your identity document.</p>
  </section>
</main>
```

Diagram:

```text
body
|
+-- header
|   +-- nav
|
+-- main
|   +-- section
|   +-- article
|   +-- aside
|
+-- footer
```

## 2. Difference Between div And Semantic Tags?

`div` is a generic container with no meaning. Semantic tags communicate purpose.

Use semantic tags when the content has meaning. Use `div` for neutral grouping or layout when no semantic element fits.

Example:

```html
<!-- Less meaningful -->
<div class="nav">
  <a href="/">Home</a>
</div>

<!-- Better -->
<nav aria-label="Main navigation">
  <a href="/">Home</a>
</nav>
```

Interview answer: Semantic tags improve machine understanding, accessibility, SEO, and developer readability. `div` is still valid, but it should not replace meaningful tags.

```text
Generic structure                  Semantic structure

div.page                           body
|-- div.header                     |-- header
|-- div.navigation                |   `-- nav
|-- div.content                    |-- main
`-- div.footer                     `-- footer

Meaning comes from classes         Meaning comes from HTML elements
```

## 3. What Is The Difference Between section And article?

`section` groups related content around one topic. `article` represents self-contained content that can stand independently.

Use `section` for page areas such as onboarding steps, dashboard areas, or grouped settings.

Use `article` for blog posts, news items, comments, product reviews, cards, or independent status updates.

Example:

```html
<section aria-labelledby="billing-heading">
  <h2 id="billing-heading">Billing Details</h2>
  <p>Update invoice and payment information.</p>
</section>

<article>
  <h2>New Payment Rules Released</h2>
  <p>This update can be shared as a standalone news item.</p>
</article>
```

Memory line:

```text
section = part of a page
article = independent content item
```

They did not directly replace one old tag. They replaced common patterns like `div class="section"` and `div class="post"` with meaningful HTML5 elements.

## 4. Can section And article Be Used Only Inside main?

No. They are commonly used inside `main`, but they can also be used inside `aside`, `footer`, or another `article` if the meaning is correct.

Example:

```html
<aside>
  <section>
    <h2>Need Help?</h2>
    <p>Contact support for onboarding assistance.</p>
  </section>
</aside>
```

Interview answer: Use tags based on meaning, not only location. `main` is for primary page content. `section` and `article` can appear wherever grouped or independent content is needed.

## 5. What Is aside?

`aside` represents complementary content related to the main content but not part of the main flow.

Examples:

- Help panel
- Related links
- Sidebar filters
- Ads
- Notes
- Author bio

Example:

```html
<aside aria-labelledby="help-heading">
  <h2 id="help-heading">Need Help?</h2>
  <p>Keep your passport and address proof ready.</p>
</aside>
```

Interview answer: I use `aside` for supporting content that helps the user but is not the main task or article content.

## 6. How Do You Improve Accessibility In HTML?

Use semantic HTML, visible labels, correct heading order, meaningful alt text, keyboard-friendly controls, clear error messages, and ARIA only when native HTML is not enough.

- `label`: gives a form control an accessible name and a larger clickable area.
- `alt`: communicates an informative image's purpose; use `alt=""` for a decorative image.
- `aria-*`: adds a name, description, relationship, or state when native HTML cannot provide it.
- Keyboard navigation: use native interactive elements such as `button` and `a`, preserve logical DOM order, and keep focus visible.
- Heading hierarchy: use headings to describe document structure, usually moving from `h1` to `h2` to `h3` without selecting levels for visual size.

Example:

```html
<main>
  <h1>Identity verification</h1>

  <section aria-labelledby="document-heading">
    <h2 id="document-heading">Upload your document</h2>
    <img src="passport-example.png" alt="Example showing the passport photo page">

    <label for="document">Identity document</label>
    <input id="document" name="document" type="file" required
           aria-describedby="document-help">
    <p id="document-help">Upload a PDF, JPG, or PNG file.</p>

    <button type="submit">Continue</button>
  </section>
</main>
```

Accessibility relationship diagram:

```text
h1 -> h2                    creates a meaningful heading hierarchy
label --for/id-----------> input receives an accessible name
aria-describedby --id----> input receives extra instructions
alt ---------------------> image receives a text alternative
Tab key -----------------> reaches the native input and button
```

Accessibility checklist:

```text
Can the user understand it?
Can the user reach it with keyboard?
Can the user operate it?
Can the user understand errors?
Can assistive technology identify name, role, and state?
```

Interview answer: I start with native HTML semantics, then verify keyboard navigation, labels, headings, focus order, and screen reader meaning.

## 7. What Are ARIA Attributes?

ARIA means Accessible Rich Internet Applications. ARIA attributes provide extra accessibility information when native HTML cannot express a custom UI pattern.

Common ARIA attributes:

- `aria-label`
- `aria-labelledby`
- `aria-describedby`
- `aria-expanded`
- `aria-controls`
- `aria-live`

Example:

```html
<button aria-expanded="false" aria-controls="account-panel">
  Account details
</button>

<section id="account-panel" aria-labelledby="account-heading">
  <h2 id="account-heading">Account Details</h2>
</section>
```

Interview answer: ARIA is useful for custom components, but native HTML should be preferred. Incorrect ARIA can make accessibility worse.

## 8. What Is aria-labelledby?

`aria-labelledby` connects an element to visible text that acts as its accessible label.

Example:

```html
<section aria-labelledby="poi-heading">
  <h2 id="poi-heading">Proof Of Identity</h2>
  <p>Upload your passport or driving license.</p>
</section>
```

Relationship diagram:

```text
section aria-labelledby="poi-heading"
                  |
                  v
        h2 id="poi-heading"
        "Proof Of Identity"
```

Real-time scenario: On a banking onboarding page, each upload panel can be labelled by its visible heading. A screen reader can announce the section as "Proof Of Identity" or "Proof Of Address."

Difference:

```text
aria-labelledby = label comes from visible text elsewhere
aria-label      = label is written directly in the attribute
```

## 9. What Is WCAG?

WCAG stands for Web Content Accessibility Guidelines. It provides standards for making web content accessible to users with disabilities.

The four principles are POUR:

```text
P = Perceivable
O = Operable
U = Understandable
R = Robust
```

Interview answer: WCAG guides frontend decisions like semantic HTML, keyboard navigation, color contrast, alt text, labels, error messages, and compatibility with assistive technologies.

## 10. How Do HTML Forms Work And How Do You Make Them Accessible?

The `form` element groups controls and defines where and how their data is submitted. On submission, successful controls are serialized as `name=value` pairs. An input without a `name` is not included in the submitted form data.

- `form`: wraps the controls and uses `action` for the destination and `method` for the HTTP method.
- `input`: collects data; its `type` affects its behavior, keyboard, and built-in validation.
- `label`: describes a control. Match its `for` value to the control's `id`.
- `name`: becomes the key sent to the server.
- `value`: becomes the value associated with that key.
- `required`: prevents normal submission while the control is empty.
- Validation: attributes such as `required`, `type`, `minlength`, `min`, and `pattern` provide browser validation. Server-side validation is still required because client-side validation can be bypassed.

Example:

```html
<form action="/applications" method="post">
  <label for="email">Email address</label>
  <input id="email" name="email" type="email" value="" required
         autocomplete="email" aria-describedby="email-help">
  <p id="email-help">Use your work email address.</p>

  <fieldset>
    <legend>Investor type</legend>
    <label>
      <input type="radio" name="investorType" value="individual">
      Individual
    </label>
    <label>
      <input type="radio" name="investorType" value="company">
      Company
    </label>
  </fieldset>

  <button type="submit">Submit application</button>
</form>
```

If the user enters `applicant@example.com` and selects `individual`, the browser constructs data equivalent to:

```text
email=applicant%40example.com&investorType=individual
```

Submission and validation flow:

```text
User fills controls
        |
        v
Browser checks required/type/other constraints
        |
   +----+----+
   |         |
 invalid    valid
   |         |
show error   v
          collect name=value pairs
                 |
                 v
          send to form action
                 |
                 v
          server validates again
```

Interview answer: A form submits its named controls as key-value pairs. I use appropriate input types and native validation for immediate feedback, but I always validate again on the server. For accessibility, every control has a visible label, related controls use `fieldset` and `legend`, errors are understandable, and keyboard operation works even when the form is rendered by React.

## 11. What Is The Difference Between label, placeholder, And aria-label?

`label` is the best visible label for a form control.

`placeholder` is only hint text inside the field. It should not replace a label.

`aria-label` gives an accessible name when no visible label exists.

Example:

```html
<label for="search">Search customers</label>
<input id="search" name="search" type="search" placeholder="Name or email">
```

Interview answer: I prefer visible labels because they help all users. Placeholder text disappears when typing and may not be enough for accessibility.

## 12. Difference Between Local Storage And Session Storage?

Both store key-value string data in the browser.

`localStorage` persists until manually cleared. `sessionStorage` lasts only for the current browser tab session.

Diagram:

```text
localStorage
browser close -> data remains

sessionStorage
tab close -> data removed
```

Example:

```html
<script>
  localStorage.setItem("theme", "dark");
  sessionStorage.setItem("currentStep", "identity");
</script>
```

Interview answer: I use local storage for non-sensitive long-lived preferences and session storage for temporary tab-specific data. I avoid storing sensitive data in either.

## 13. Difference Between Cookies And Local Storage?

Cookies can be sent with HTTP requests. Local Storage stays in the browser and is accessed by JavaScript.

Diagram:

```text
Cookie
Browser <----> Server
sent with matching HTTP requests

Local Storage
Browser only
not automatically sent to server
```

Example:

```html
<script>
  document.cookie = "theme=dark; path=/; max-age=3600; SameSite=Lax";
  localStorage.setItem("theme", "dark");
</script>
```

Interview answer: Cookies are useful for server-aware data and can use security flags like `HttpOnly`, `Secure`, and `SameSite`. Local Storage is useful for non-sensitive client preferences.

## 14. Difference Between id And class?

`id` uniquely identifies one element. `class` groups one or more elements.

Example:

```html
<h1 id="page-title">Dashboard</h1>
<p class="status-message">Approved</p>
<p class="status-message">Pending</p>
```

Use `id` for unique anchors, form label connections, and ARIA relationships. Use `class` for reusable styling or behavior.

```text
id="email"       -> one unique element -> label/ARIA/anchor target
class="field"    -> many elements      -> shared styling or behavior
```

Interview answer: An `id` should be unique in the document. A `class` can be reused across multiple elements.

## 15. Difference Between Block, Inline, And Inline-block?

Block elements start on a new line and take the available width. Inline elements flow inside text. Inline-block elements flow inline but can accept width and height.

Diagram:

```text
block:
[ full row element        ]
[ another full row        ]

inline:
Text [span] continues in the same line

inline-block:
[box] [box] [box]
inline flow, box dimensions allowed
```

Example:

```html
<div>Block element</div>
<span>Inline element</span>
<button>Inline-block-like control</button>
```

Interview answer: Block is used for layout structure, inline for text-level content, and inline-block when an element should stay inline but behave like a box.

## 16. What Is The Difference Between async And defer?

Both load external scripts without blocking HTML parsing.

`async` executes as soon as the script downloads. Script order is not guaranteed.

`defer` executes after HTML parsing finishes. Script order is preserved.

Diagram:

```text
Normal script:
HTML parse -> stop -> download -> execute -> continue parse

async:
HTML parse + download in parallel -> execute immediately when ready

defer:
HTML parse + download in parallel -> execute after HTML parse
```

Example:

```html
<script src="analytics.js" async></script>
<script src="app.js" defer></script>
```

Interview answer: I use `defer` for most application scripts because it preserves order and runs after parsing. I use `async` for independent scripts like analytics.

## 17. How Do You Improve SEO Using HTML?

Use proper title, meta description, semantic HTML, correct heading hierarchy, descriptive links, meaningful alt text, canonical URLs, and structured data when relevant.

Example:

```html
<head>
  <title>HTML Interview Preparation</title>
  <meta name="description" content="Practice HTML interview questions with examples.">
  <link rel="canonical" href="https://example.com/html-interview">
</head>
```

Interview answer: SEO-friendly HTML gives search engines a clear structure and meaning. Accessibility and performance also support a better user experience, which indirectly helps SEO.

## 18. What Are HTML5 APIs?

HTML5 APIs are browser capabilities exposed to web applications.

Examples:

- Web Storage API
- Geolocation API
- Canvas API
- Drag and Drop API
- History API
- File API
- Media APIs
- Web Workers

Example:

```html
<script>
  history.pushState({ page: "profile" }, "", "#profile");

  if ("geolocation" in navigator) {
    console.log("Geolocation is supported");
  }
</script>
```

Interview answer: HTML5 APIs allow web apps to use browser-native features like storage, location, media, files, graphics, and background processing.

## 19. What Is The Purpose Of The alt Attribute?

`alt` provides alternative text for images. It helps screen reader users and appears if the image fails to load.

Example:

```html
<img src="kyc-status.png" alt="KYC application status showing pending verification">
```

Decorative image:

```html
<img src="divider.png" alt="">
```

Interview answer: Informative images need meaningful alt text. Decorative images should use empty alt text so assistive technologies can skip them.

## 20. What Are data Attributes?

`data-*` attributes store custom, non-sensitive metadata on HTML elements.

Example:

```html
<button data-action="approve" data-request-id="REQ-1024">
  Approve request
</button>

<script>
  const button = document.querySelector("[data-action]");
  console.log(button.dataset.action);
  console.log(button.dataset.requestId);
</script>
```

Attribute-to-JavaScript mapping:

```text
HTML attribute             dataset property
data-action          --->  element.dataset.action
data-request-id      --->  element.dataset.requestId
                           kebab-case becomes camelCase
```

Interview answer: Data attributes are useful for small metadata, testing hooks, analytics, and progressive enhancement. I avoid storing sensitive data or complex application state in them.

## 21. What Is The Purpose Of doctype?

`<!DOCTYPE html>` tells the browser to render the page in standards mode.

Example:

```html
<!DOCTYPE html>
<html lang="en">
  ...
</html>
```

Interview answer: The doctype prevents quirks mode and helps browsers render HTML and CSS consistently.

## 22. Why Is lang Important On The html Tag?

The `lang` attribute declares the page language.

Example:

```html
<html lang="en">
```

Interview answer: It helps screen readers pronounce content correctly, helps search engines understand language, and improves accessibility.

## 23. What Is The viewport Meta Tag?

The viewport meta tag controls layout on mobile devices.

Example:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Interview answer: It tells the browser to match the viewport width to the device width and start at normal zoom. Without it, responsive layouts may not work properly on mobile.

## 24. What Is The Difference Between head And body?

`head` contains metadata and resources for the document. `body` contains visible page content.

Example:

```html
<head>
  <title>Dashboard</title>
  <meta name="description" content="Account dashboard">
</head>
<body>
  <h1>Dashboard</h1>
</body>
```

Interview answer: `head` describes the document. `body` displays the document content.

## 25. What Is Heading Hierarchy?

Heading hierarchy means using headings in a logical order from `h1` to `h6`.

Example:

```html
<h1>Account Dashboard</h1>
<h2>Verification</h2>
<h3>Proof Of Identity</h3>
```

Diagram:

```text
h1 Page title
|
+-- h2 Major section
|   +-- h3 Subsection
|
+-- h2 Another major section
```

Interview answer: Correct heading hierarchy improves accessibility, readability, and SEO. I do not choose heading levels only for visual size.

## 26. What Are void Elements?

Void elements do not have closing tags and cannot contain child content.

Examples:

```html
<img src="profile.png" alt="User profile photo">
<input type="text" name="firstName">
<br>
<hr>
<meta charset="UTF-8">
<link rel="stylesheet" href="styles.css">
```

Interview answer: Void elements are self-contained HTML elements. They should not be written with separate closing tags.

## 27. Difference Between button And input type="button"?

Both can create buttons, but `button` is more flexible because it can contain text and other inline content.

Example:

```html
<button type="submit">Submit application</button>
<input type="button" value="Cancel">
```

Interview answer: I prefer `button` for most UI actions because it is more flexible and readable. I always specify `type` to avoid accidental form submission.

## 28. What Is The Difference Between GET And POST In Forms?

`GET` sends form data in the URL query string. `POST` sends form data in the request body.

Example:

```html
<form method="get" action="/search">
  <input name="query" type="search">
</form>

<form method="post" action="/applications">
  <input name="email" type="email">
</form>
```

Interview answer: I use `GET` for safe, shareable, bookmarkable requests like search. I use `POST` for submissions that create or update data.

## 29. What Are Common HTML Form Input Types?

Common types include `text`, `email`, `password`, `number`, `tel`, `url`, `date`, `file`, `checkbox`, `radio`, `search`, and `submit`.

Example:

```html
<input type="email" autocomplete="email">
<input type="tel" autocomplete="tel">
<input type="file" accept=".pdf,.jpg,.png">
```

Interview answer: Choosing the correct input type improves validation, accessibility, mobile keyboard behavior, and user experience.

## 30. What Is Native HTML Validation?

Native validation uses built-in HTML attributes to validate form input.

Examples:

```html
<input type="email" required>
<input type="text" minlength="3" maxlength="50">
<input type="number" min="1" max="100">
<input type="text" pattern="[A-Za-z ]+">
```

Interview answer: Native validation is useful for basic client-side checks, but important validation must also happen on the server.

## 31. What Is The Difference Between strong And b?

`strong` communicates importance. `b` only applies stylistic bold text without importance.

Example:

```html
<p><strong>Warning:</strong> Your session will expire soon.</p>
<p><b>Label:</b> Premium customer</p>
```

Interview answer: I use `strong` when the content is important and `b` only when visual bolding is needed without semantic importance.

## 32. What Is The Difference Between em And i?

`em` communicates emphasis. `i` represents text in an alternate voice, such as a technical term, phrase, or title.

Example:

```html
<p>You <em>must</em> upload a valid document.</p>
<p>The term <i>responsive design</i> is common in frontend interviews.</p>
```

Interview answer: I use `em` for meaningful emphasis and `i` for alternate text style when emphasis is not intended.

## 33. What Are Responsive Images?

Responsive images allow the browser to choose the best image for the device and viewport.

Example:

```html
<img
  src="profile-800.jpg"
  srcset="profile-400.jpg 400w, profile-800.jpg 800w"
  sizes="(max-width: 600px) 400px, 800px"
  alt="Customer profile summary"
>
```

Interview answer: Responsive images improve performance by avoiding unnecessarily large image downloads, especially on mobile.

## 34. What Is The picture Element?

`picture` provides multiple image sources for art direction or format support.

Example:

```html
<picture>
  <source srcset="dashboard.avif" type="image/avif">
  <source srcset="dashboard.webp" type="image/webp">
  <img src="dashboard.jpg" alt="Dashboard summary">
</picture>
```

Interview answer: I use `picture` when the image itself needs to change by format or layout, not just size.

## 35. How Do You Improve HTML Performance?

Use semantic and minimal markup, optimized images, lazy loading, `defer` scripts, preconnect/preload where useful, and avoid unnecessary DOM depth.

Example:

```html
<link rel="preconnect" href="https://fonts.example.com">
<link rel="preload" href="/hero.webp" as="image">
<img src="report.webp" alt="Monthly report chart" width="800" height="400" loading="lazy">
<script src="/app.js" defer></script>
```

Interview answer: HTML performance is about helping the browser discover resources efficiently and avoiding layout shifts from missing image dimensions.

## 36. What Is iframe?

`iframe` embeds another HTML page inside the current page.

Example:

```html
<iframe
  src="https://example.com"
  title="Example embedded page"
  loading="lazy">
</iframe>
```

Interview answer: I use iframes carefully because they can affect performance, security, and accessibility. A meaningful `title` is important for screen reader users.

## 37. What Is The Difference Between script, noscript, And template?

`script` runs JavaScript. `noscript` provides fallback content when JavaScript is disabled. `template` stores inert HTML that JavaScript can clone later.

Example:

```html
<noscript>Please enable JavaScript to use this application.</noscript>

<template id="row-template">
  <tr>
    <td></td>
  </tr>
</template>
```

Interview answer: These tags help manage JavaScript-driven behavior and fallbacks while keeping HTML meaningful.

## 38. What Is The Difference Between Relative And Absolute URLs?

An absolute URL includes the full protocol and domain. A relative URL depends on the current location.

Example:

```html
<a href="https://example.com/docs">Absolute URL</a>
<a href="/docs">Root-relative URL</a>
<a href="docs/page.html">Relative URL</a>
```

Interview answer: I use absolute URLs for external destinations and relative/root-relative URLs for internal project paths.

## 39. What Are Accessible Tables?

Accessible tables use proper table structure and header relationships.

Example:

```html
<table>
  <caption>Recent transactions</caption>
  <thead>
    <tr>
      <th scope="col">Date</th>
      <th scope="col">Merchant</th>
      <th scope="col">Amount</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>2026-07-04</td>
      <td>Utility Payment</td>
      <td>1200</td>
    </tr>
  </tbody>
</table>
```

Interview answer: Tables should be used for tabular data, not page layout. I use `caption`, `th`, and `scope` to make relationships clear.

## 40. What Is Good HTML In A React Application?

Good HTML in React means the rendered DOM remains semantic, accessible, and valid.

Example:

```jsx
function SubmitButton() {
  return <button type="submit">Submit application</button>;
}
```

Avoid:

```jsx
function SubmitButton() {
  return <div onClick={submit}>Submit application</div>;
}
```

Interview answer: Even in React, the browser receives HTML. I make sure components render correct elements, labels, landmarks, headings, buttons, and form controls.

## Final Revision Cheat Sheet

```text
Semantic HTML:
Use meaningful tags.

Accessibility:
Name, role, state, keyboard, focus, labels.

ARIA:
Use only when native HTML is not enough.

Forms:
label + input + help text + error message.

Storage:
localStorage persists, sessionStorage is tab/session scoped, cookies can go to server.

Scripts:
async = execute when ready, defer = execute after parse in order.

SEO:
title, meta description, headings, semantic structure, alt text.

Performance:
defer scripts, optimize images, add dimensions, lazy load, reduce DOM depth.
```
