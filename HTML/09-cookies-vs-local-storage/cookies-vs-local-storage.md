# Cookies vs Local Storage

## What It Means

Cookies and local storage both store data in the browser, but they are used differently.

## Difference

Cookies are sent with HTTP requests. They can include security options like `HttpOnly`, `Secure`, and `SameSite`.

Local Storage is not automatically sent to the server and is accessible through JavaScript.

## Interview Answer

Cookies are useful when the server needs the data on requests, especially for session-related behavior with secure flags. Local storage is useful for non-sensitive client-side preferences. I avoid storing sensitive data in local storage because it is accessible by JavaScript.

## Quick Revision

Cookies travel with requests. Local storage stays in the browser.
