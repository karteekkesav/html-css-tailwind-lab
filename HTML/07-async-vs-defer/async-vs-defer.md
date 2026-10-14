# async vs defer

## What It Means

`async` and `defer` are attributes for external scripts. They allow the browser to download scripts without blocking HTML parsing.

## Difference

`async` executes as soon as the script is downloaded. Execution order is not guaranteed.

`defer` executes after the HTML is parsed. Execution order is preserved.

## Interview Answer

I use `defer` for most application scripts because it waits until HTML parsing is complete and keeps scripts in order. I use `async` for independent scripts like analytics where order does not matter.

## Quick Revision

`async`: independent and execute when ready. `defer`: ordered and execute after parsing.
