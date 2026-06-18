# HTX Realty — Newsletters

Source files for HTX Realty Group's weekly email newsletters, built as
[Brevo](https://www.brevo.com/)-ready HTML and sent each week.

## Repository layout

```
newsletters/
├── brand/                         Shared assets, reused in every edition
│   ├── htx-logo.png               Full HTX Realty Group logo  → ##LOGO##
│   └── vamshi-kyatham-headshot.png  Agent headshot (optional use)
├── templates/
│   └── brevo-newsletter.template.html   Master layout to copy each week
└── editions/
    └── <year>/
        └── <YYYY-MM-DD-slug>/      One folder per weekly send
            ├── newsletter.html     The Brevo-import HTML for that edition
            ├── images/             Property photos for that edition only
            └── README.md           Subject line, preview text, send notes
```

## Naming convention

Each edition lives in `editions/<year>/<YYYY-MM-DD>-<short-slug>/`, where the
date is the **send date** and the slug describes the feature (e.g.
`2026-06-17-1216-hwy-87-beach-house`). Dated folders sort chronologically and
keep every edition self-contained.

## Producing a new edition

1. **Copy the template** into a new dated folder:
   ```
   cp templates/brevo-newsletter.template.html \
      editions/2026/2026-06-24-my-slug/newsletter.html
   ```
2. **Drop the photos** into that edition's `images/` folder.
3. **Edit the copy** — headline, address, price, specs, and any deal-specific
   figures — directly in `newsletter.html`.
4. **Upload the images** to Brevo's content library (or any public host) and
   find-and-replace the `##TOKEN##` placeholders with the hosted URLs. The
   token → image mapping is listed in the comment block at the top of each
   `newsletter.html`.
5. **Import into Brevo**, set the subject line / preview text (record them in
   the edition's `README.md`), test, and send.

## Image tokens

Every `newsletter.html` references images by placeholder so the layout can be
designed before assets are hosted:

| Token        | Image                              |
|--------------|------------------------------------|
| `##LOGO##`   | `brand/htx-logo.png`               |
| `##HERO##`   | edition `images/` — hero photo     |
| `##BEACH##`  | edition `images/` — secondary photo|
| `##GRID1##`–`##GRID4##` | edition `images/` — 2×2 photo grid |
| `##EMBLEM##` | small HTX mark (crop from the logo)|

## What's public vs. local

This repo is public, so it contains only what's needed to view and reproduce a
newsletter — HTML, brand assets, and property photos. Internal material
(recipient lists, drafts, analytics, agent config) is excluded via
[`.gitignore`](.gitignore). Keep private notes in an `_internal/` folder or a
`*.local.md` file and they will not be committed.
