# Lab: Unprotected admin functionality with unpredictable URL

**Level:** Apprentice
**Topic:** Access control

## What the lab asks

The admin panel is unprotected again, but this time its URL is a random, unpredictable string (for example `/admin-qm0k2o`). The task is to find the panel and delete `carlos`.

## How I solved it

1. This time `robots.txt` and a plain `/admin` didn't help — the URL was random.
2. I opened the home page source (right-click → "View Page Source", or Ctrl+U).
3. The admin panel URL was hidden inside the JavaScript — the site didn't show it, but it was left in the code:
   ```
   /admin-qm0k2o
   ```
4. I went to that URL and the panel opened.
5. I clicked "Delete" next to `carlos`.

"User deleted successfully" appeared, and the lab was marked "Solved".

**Screenshot:** put it in the `screenshots/` folder — name it `02-unpredictable-url-solved.png`.

## Why it matters

Making the URL random isn't full protection either. If the URL leaks anywhere (page source, JavaScript, comments), an attacker will find it. The only real protection is checking access rights on the server side.

## How to fix it

- Don't leak the admin URL in the code.
- Most importantly: don't rely on hiding the URL — add a proper role/permission check on the server side.
