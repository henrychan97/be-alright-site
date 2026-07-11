# Be Alright Tutoring — /explore

Static consultation presentation page for **start.bealrighttutoring.com/explore**.

## Deploy
Upload this whole `explore/` folder to the root of the GitHub repo that serves
`start.bealrighttutoring.com`. GitHub Pages will serve it at:

```
https://start.bealrighttutoring.com/explore/
```

`index.html` loads automatically at that path. All images are self-contained in `assets/`
(relative paths), so nothing else is needed — no build step, no dependencies.

## Files
- `index.html` — the full scroll-through presentation.
- `assets/` — logo, Dr. Meg photo, tutor photos, reading-report score cards, and parent testimonials.

## Adding Bob's photo later
Bob Nieman currently shows a branded **"BN"** initials avatar. To use his real photo:
1. Add a square headshot as `assets/tutor-bob.jpg`.
2. In `index.html`, find `<div class="tavatar" role="img" aria-label="Bob Nieman">BN</div>`
   and replace it with:
   `<img class="tphoto" src="assets/tutor-bob.jpg" alt="Bob Nieman">`

## Note
The testimonials and student score cards use real family/first names. Make sure you have
consent to display these publicly before the page goes live.
