# HTML, CSS & Tailwind CSS Interview Prep

A hands-on study lab for front-end interview preparation. It covers **HTML**, **CSS**, and **Tailwind CSS**. Every topic has two files:

- a runnable `.html` demo you can open in the browser and experiment with
- a `.md` note with the explanation, a ready-to-say interview answer, common mistakes, and revision points

There is nothing to install or build. It's plain HTML and CSS, and the Tailwind demos load Tailwind from its CDN.

---

## Getting Started

### Prerequisites

- [Git](https://git-scm.com/downloads)
- Any modern web browser (Chrome, Firefox, Edge, Safari)
- *(Optional)* [VS Code](https://code.visualstudio.com/) with the [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) extension, or Python 3 for a local server

### 1. Clone the repository

```bash
git clone https://github.com/karteekkesav/<repo-name>.git
cd <repo-name>
```

> Replace `<repo-name>` with the name of this repository. You can also click the green **Code** button on GitHub and copy the URL.

No Git? Click **Code → Download ZIP** on GitHub and extract it.

### 2. Open a demo

Pick whichever option you prefer.

**Option A: Open the file directly**

Double-click any `.html` file, for example `HTML/01-semantic-html/semantic-html.html`. It opens in your default browser.

**Option B: VS Code Live Server (auto-reloads on save)**

1. Open the project folder in VS Code.
2. Right-click any `.html` file and choose **Open with Live Server**.

**Option C: Python local server**

From the project root:

```bash
python -m http.server 5500
```

Then open a topic in your browser, for example:

```text
http://localhost:5500/CSS/04-flexbox/flexbox.html
```

> Folder names with spaces (like `Tailwind CSS`) are URL-encoded as `%20`, e.g. `http://localhost:5500/Tailwind%20CSS/01-utility-first-basics/utility-first-basics.html`.

> **Note:** The Tailwind CSS demos load Tailwind from `https://cdn.tailwindcss.com`, so they need an internet connection to render their styles.

### 3. Read the notes

Open the matching `.md` file next to each demo. It renders well on GitHub or in VS Code's Markdown preview (`Ctrl+Shift+V` / `Cmd+Shift+V`).

---

## Project Structure

```text
.
├── HTML/
│   ├── html-roadmap.md                 # Study order and practice method
│   ├── html-interview-questions.md     # Master Q&A revision guide
│   └── NN-topic-name/
│       ├── topic-name.html             # Runnable demo
│       └── topic-name.md               # Notes and interview answer
├── CSS/
│   ├── css-roadmap.md
│   ├── css-interview-questions.md
│   └── NN-topic-name/ ...
└── Tailwind CSS/
    ├── tailwind-roadmap.md
    ├── tailwind-interview-questions.md
    └── NN-topic-name/ ...
```

---

## Topics

### HTML (15 topics)

| # | Topic |
|---|-------|
| 01 | [Semantic HTML](HTML/01-semantic-html/semantic-html.md) |
| 02 | [div vs Semantic Tags](HTML/02-div-vs-semantic-tags/div-vs-semantic-tags.md) |
| 03 | [Accessibility Basics](HTML/03-accessibility-basics/accessibility-basics.md) |
| 04 | [ARIA Attributes](HTML/04-aria-attributes/aria-attributes.md) |
| 05 | [WCAG Basics](HTML/05-wcag-basics/wcag-basics.md) |
| 06 | [Forms Accessibility](HTML/06-forms-accessibility/forms-accessibility.md) |
| 07 | [async vs defer](HTML/07-async-vs-defer/async-vs-defer.md) |
| 08 | [Local Storage vs Session Storage](HTML/08-local-vs-session-storage/local-vs-session-storage.md) |
| 09 | [Cookies vs Local Storage](HTML/09-cookies-vs-local-storage/cookies-vs-local-storage.md) |
| 10 | [id vs class](HTML/10-id-vs-class/id-vs-class.md) |
| 11 | [Block, Inline & Inline-Block](HTML/11-block-inline-inline-block/block-inline-inline-block.md) |
| 12 | [SEO Basics](HTML/12-seo-basics/seo-basics.md) |
| 13 | [HTML5 APIs](HTML/13-html5-apis/html5-apis.md) |
| 14 | [alt Attribute](HTML/14-alt-attribute/alt-attribute.md) |
| 15 | [data-* Attributes](HTML/15-data-attributes/data-attributes.md) |

Roadmap: [html-roadmap.md](HTML/html-roadmap.md) · Q&A: [html-interview-questions.md](HTML/html-interview-questions.md)

### CSS (15 topics)

| # | Topic |
|---|-------|
| 01 | [Selectors & Specificity](CSS/01-css-selectors-specificity/css-selectors-specificity.md) |
| 02 | [Box Model](CSS/02-box-model/box-model.md) |
| 03 | [Display & Positioning](CSS/03-display-positioning/display-positioning.md) |
| 04 | [Flexbox](CSS/04-flexbox/flexbox.md) |
| 05 | [CSS Grid](CSS/05-css-grid/css-grid.md) |
| 06 | [Responsive Design](CSS/06-responsive-design/responsive-design.md) |
| 07 | [CSS Units](CSS/07-css-units/css-units.md) |
| 08 | [Typography](CSS/08-typography/typography.md) |
| 09 | [Colors & Backgrounds](CSS/09-colors-backgrounds/colors-backgrounds.md) |
| 10 | [Pseudo-classes & Pseudo-elements](CSS/10-pseudo-classes-elements/pseudo-classes-elements.md) |
| 11 | [Transitions & Animations](CSS/11-transitions-animations/transitions-animations.md) |
| 12 | [Forms, Focus & Accessibility](CSS/12-forms-focus-accessibility/forms-focus-accessibility.md) |
| 13 | [CSS Variables & Theming](CSS/13-css-variables-theming/css-variables-theming.md) |
| 14 | [z-index & Stacking Context](CSS/14-z-index-stacking-context/z-index-stacking-context.md) |
| 15 | [CSS Performance & Architecture](CSS/15-css-performance-architecture/css-performance-architecture.md) |

Roadmap: [css-roadmap.md](CSS/css-roadmap.md) · Q&A: [css-interview-questions.md](CSS/css-interview-questions.md)

### Tailwind CSS (8 topics)

| # | Topic |
|---|-------|
| 01 | [Utility-First Basics](Tailwind%20CSS/01-utility-first-basics/utility-first-basics.md) |
| 02 | [Spacing, Sizing & Typography](Tailwind%20CSS/02-spacing-sizing-typography/spacing-sizing-typography.md) |
| 03 | [Flex & Grid Layouts](Tailwind%20CSS/03-flex-grid-layouts/flex-grid-layouts.md) |
| 04 | [Responsive Design](Tailwind%20CSS/04-responsive-design/responsive-design.md) |
| 05 | [States & Pseudo-classes](Tailwind%20CSS/05-states-pseudo-classes/states-pseudo-classes.md) |
| 06 | [Forms & Accessibility](Tailwind%20CSS/06-forms-accessibility/forms-accessibility.md) |
| 07 | [Customization & Config](Tailwind%20CSS/07-customization-config/customization-config.md) |
| 08 | [Component Patterns & Performance](Tailwind%20CSS/08-component-patterns-performance/component-patterns-performance.md) |

Roadmap: [tailwind-roadmap.md](Tailwind%20CSS/tailwind-roadmap.md) · Q&A: [tailwind-interview-questions.md](Tailwind%20CSS/tailwind-interview-questions.md)

---

## How to Study

1. Start with the **roadmap** in each folder and follow the recommended order: HTML, then CSS, then Tailwind CSS.
2. For each topic, open the `.html` demo, read the `.md` note, then edit the demo and refresh to see what changes.
3. Practise saying the interview answer out loud.
4. Revise with the **interview-questions** file before an interview.

---

## Contributing

Suggestions and fixes are welcome.

1. Fork the repository.
2. Create a branch: `git checkout -b improve-flexbox-notes`
3. Commit your changes: `git commit -m "Clarify flex-basis example"`
4. Push the branch and open a Pull Request.

When adding a new topic, follow the existing pattern: create a `NN-topic-name/` folder with `topic-name.html` and `topic-name.md`, then add it to that folder's roadmap and to the tables above.

---

## Author

GitHub: [@karteekkesav](https://github.com/karteekkesav)
