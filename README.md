# Be Alright Tutoring — Funnel Site

All four funnel pages in one project, served under a single domain
(`go.bealrighttutoring.org`). Each page is in its own folder and is served at
the matching clean path automatically — no extra configuration needed.

## Pages & paths

| URL                                      | Folder        | Page                    |
|------------------------------------------|---------------|-------------------------|
| `go.bealrighttutoring.org/`              | (root)        | VSL / landing page      |
| `go.bealrighttutoring.org/form`          | `form/`       | Application (Typeform)  |
| `go.bealrighttutoring.org/calendar`      | `calendar/`   | Booking (Go High Level) |
| `go.bealrighttutoring.org/thank-you`     | `thank-you/`  | Thank-you (videos)      |

## Funnel wiring

- The VSL page's call-to-action buttons all link to `/form`.
- After the Typeform on `/form` is submitted, send people to `/calendar`
  (set this redirect inside Typeform).
- After the booking on `/calendar` is completed, send people to `/thank-you`
  (set this redirect inside Go High Level).

## Tracking

The Meta Pixel (ID `1555926178296998`) is installed on **every page** and fires
a `PageView` on each visit. The `/thank-you` page additionally fires a
`Schedule` event on load, so every thank-you view is counted as a scheduled
appointment in Meta.

## Structure

```
.
├── index.html            # VSL (served at /)
├── assets/img/
├── form/index.html       # served at /form
│   └── assets/img/
├── calendar/index.html   # served at /calendar
│   └── assets/img/
└── thank-you/index.html  # served at /thank-you  (+ Meta Pixel)
    └── assets/img/
```

## View locally

Clean URLs like `/form` need a server (opening files directly won't map paths):

```bash
python3 -m http.server 8000
# visit http://localhost:8000  (and /form, /calendar, /thank-you)
```

## Deploy on Vercel

1. Push this repo to GitHub and import it as **one** Vercel project
   (Framework Preset: **Other** — plain static HTML).
2. In the project: **Settings → Domains → Add** `go.bealrighttutoring.org`.
   A domain can belong to only one project, so remove it from any older
   project first.
3. Vercel serves `/`, `/form`, `/calendar`, and `/thank-you` from the matching
   folders automatically.
