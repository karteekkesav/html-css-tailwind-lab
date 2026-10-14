# Tailwind Component Patterns And Performance

## What It Means

Tailwind works well with component-based frameworks like React. The goal is to keep utility classes readable and reusable.

## React Component Pattern

```jsx
function Button({ children, variant = "primary" }) {
  const variants = {
    primary: "bg-blue-600 text-white hover:bg-blue-700",
    secondary: "border border-slate-300 text-slate-700 hover:bg-slate-50"
  };

  return (
    <button className={`rounded-md px-4 py-2 font-medium ${variants[variant]}`}>
      {children}
    </button>
  );
}
```

## Why This Helps

```text
reuse button styles
avoid copying long class strings everywhere
keep variants predictable
make interview examples cleaner
```

## Performance

In production builds, Tailwind scans source files and generates CSS only for used classes.

```text
development = many utilities available
production  = unused CSS removed
```

## Common Mistake

Avoid building class names dynamically in a way Tailwind cannot detect.

Risky:

```jsx
<div className={`bg-${color}-600`}>...</div>
```

Better:

```jsx
const colors = {
  blue: "bg-blue-600",
  green: "bg-green-600"
};
```

## Interview Answer

In React, I use Tailwind directly for simple components and extract reusable components when class strings repeat. For performance, Tailwind generates only used CSS in production, but I avoid unpredictable dynamic class names so the build can detect required utilities.
