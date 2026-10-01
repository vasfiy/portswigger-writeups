# Lab: Unprotected admin functionality

**Level:** Apprentice
**Topic:** Access control

## What the lab asks

The site has an unprotected admin panel. The task is to find it and delete the user `carlos`.

## How I solved it

1. The admin panel wasn't shown in the menu, but it had to live at some URL.
2. I opened the site's `robots.txt` file:
   ```
   /robots.txt
   ```
   It had the admin panel path inside:
   ```
   Disallow: /administrator-panel
   ```
3. I went straight to that path:
   ```
   /administrator-panel
   ```
   The panel opened without even asking for a login — no protection at all.
4. From the user list, I clicked "Delete" next to `carlos`.

"User deleted successfully" appeared, and the lab was marked "Solved".

**Screenshot:** put it in the `screenshots/` folder — name it `01-user-deleted.png` (showing "User deleted successfully" and the "Solved" banner).

## Why it matters

The site thought hiding the admin panel was enough to protect it. But hiding is not protecting. Anyone who knows the URL can get in and delete users. This is the number one issue in the OWASP Top 10 (Broken Access Control).

## How to fix it

- Check on the server side that only admin users can reach admin functions.
- Don't confuse "hiding" with "protecting".
- Every sensitive page needs a role check.
