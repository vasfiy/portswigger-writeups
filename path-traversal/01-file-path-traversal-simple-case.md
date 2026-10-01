# Lab: File path traversal, simple case

**Level:** Apprentice
**Topic:** Path traversal

## What the lab asks

The site shows product images that load through a `filename` parameter. The task is to read the `/etc/passwd` file.

## How I solved it

1. I opened a product on the site ("View details").
2. I right-clicked the image and opened it in a new tab. The URL looked like this:
   ```
   /image?filename=52.jpg
   ```
3. So the site takes a file name and reads it directly. There was no protection, so I changed the `filename` value:
   ```
   /image?filename=../../../etc/passwd
   ```
4. `../` means going one folder up. With three of them I reached the filesystem root and got to `/etc/passwd`.
5. The browser tried to open the file as an image and showed a "broken image" icon. So I added `view-source:` in front of the URL and saw the file contents:
   ```
   root:x:0:0:root:/root:/bin/bash
   daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
   ...
   ```

The lab was marked "Solved".

**Screenshot:** put it in the `screenshots/` folder — name it `01-passwd-output.png` (the `/etc/passwd` output shown through view-source).

## Why it matters

Without protection, an outsider can read any file on the server — config files, secret keys, user data. Here `/etc/passwd` even showed real users like `peter`, `carlos`, and `user`.

## How to fix it

- Don't use a user-supplied file name directly.
- Strip `../` and similar sequences from the file name.
- Make sure files are only read from an allowed folder (canonical path check).
