# Local Storage vs Session Storage

## What It Means

Both are Web Storage APIs that store string key-value pairs in the browser.

## Difference

`localStorage` persists until cleared.

`sessionStorage` persists only for the current browser tab session.

## Interview Answer

I use local storage for non-sensitive preferences that should remain after the browser closes, such as theme choice. I use session storage for temporary tab-specific data. I avoid storing sensitive information in either because JavaScript can access both.

## Quick Revision

Local means persistent. Session means tab/session lifetime.
