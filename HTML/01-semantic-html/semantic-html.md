# Semantic HTML

## What It Means

Semantic HTML uses elements that describe the purpose of content.

Examples: `header`, `nav`, `main`, `section`, `article`, `aside`, and `footer`.

## Tags Used In This Example

### `header`

Represents introductory content for the page or a section. In this example, it contains the portal title and main navigation.

### `nav`

Represents a group of navigation links. Use it for important navigation areas, not every random group of links.

### `main`

Represents the primary unique content of the page. A page should usually have only one visible `main`.

### `section`

Groups related content around one topic. In this example, `Proof Of Identity` and `Proof Of Address` are sections because they are parts of the onboarding flow.

### `article`

Represents self-contained content that can stand independently. Examples include blog posts, news cards, comments, product reviews, or independent status updates.

In this example, `Application Review` is shown as an `article` to demonstrate a self-contained status/update block. If you treat it only as another onboarding step, using `section` would also be acceptable.

### `aside`

Represents complementary content related to the main content, but not part of the main flow. Examples include help panels, sidebars, related links, notes, ads, or tips.

In this example, `Need Help?` is an `aside` because it supports the onboarding flow but is not one of the required onboarding steps.

### `footer`

Represents footer content for the page or a section. It commonly contains copyright text, secondary links, contact details, or legal information.

## Why It Matters

Semantic HTML improves accessibility, SEO, code readability, and maintainability. It also helps React components produce meaningful markup instead of deeply nested generic containers.

## Interview Answer

Semantic HTML is the practice of using meaningful HTML tags that explain the role of content. For example, I use `nav` for navigation, `main` for the primary page content, and `article` for reusable content blocks. This helps browsers, screen readers, search engines, and developers understand the page structure.

## Common Mistakes

- Using `div` for everything.
- Skipping the `main` element.
- Using headings only for visual size instead of document structure.
- Placing multiple unrelated concepts inside one generic section.

## Quick Revision

Semantic HTML answers the question: "What is this content?" not "How should it look?"
