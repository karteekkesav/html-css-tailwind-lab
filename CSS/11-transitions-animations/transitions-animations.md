# Transitions And Animations

## What It Means

Transitions animate property changes between states. Animations use `@keyframes` for multi-step motion.

## Diagram

```text
transition:
normal state -> hover/focus state

animation:
0% -> 50% -> 100%
```

## Resume-Based Example

Use subtle transitions for buttons, cards, progress states, and validation feedback. Avoid motion that harms accessibility.

## Interview Answer

I use transitions for simple state changes and animations for more complex motion. For performance, I prefer animating `transform` and `opacity`.

## Accessibility Note

Respect `prefers-reduced-motion`.
