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

All Meta tracking runs through Google Tag Manager container `GTM-5TTWDZTV`
(pixel/dataset `1555926178296998`). The same container is on beontrackedu.com.
There is no hard-coded pixel snippet in these pages; do not add one.

- PageView: GTM Meta Pixel tag on every page, mirrored server-side by the Stape
  data tag (sGTM at rrvqewob.usv.stape.io) with the same event_id.
- Lead: fires on every Typeform submit, including "not a fit" endings.
- Schedule: fires once per booking, when the GHL booking iframe posts
  `msgsndr-booking-complete` to the page (/calendar, /calendar-l, and
  beontrackedu.com/calendar). Browser and Stape server copies share one
  event_id so Meta deduplicates them. /thank-you does NOT fire Schedule, so
  refreshing or revisiting it never adds a booking.
- Schedule is one event name for three calendars (Meg, Bella, Be On Track).
  Split them in Meta with custom conversions (URL contains
  start.bealrighttutoring.org/calendar and not calendar-l = Meg;
  calendar-l = Bella; beontrackedu.com = Be On Track).

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
