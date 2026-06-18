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
3. **Fill in the copy** — the template ships blank, with every headline,
   address, price, stat, figure, and body paragraph written as a `##TOKEN##`
   placeholder. Find-and-replace each token with that week's content. The full
   token reference (grouped by section, with example values) lives in the
   comment block at the top of the template. Sections are modular — delete any
   `<tr>` you don't need that week (e.g. the cost-seg ledger).
4. **Upload the images** to Brevo's content library (or any public host) and
   find-and-replace the image `##TOKEN##` placeholders with the hosted URLs.
5. **Import into Brevo**, set the subject line / preview text (record them in
   the edition's `README.md`), test, and send.

## Tokens

The template's copy is fully tokenized — every headline, stat, and figure is a
`##TOKEN##` placeholder, so the layout can be built before any content exists.
The **authoritative, grouped list with example values is in the comment block
at the top of `templates/brevo-newsletter.template.html`.** Content tokens
cover the edition label/date, eyebrows, headlines, address, price, specs, the
cost-seg ledger figures, the six feature cards, the four selling points, and
the footer disclaimer.

The **images** are wired to labelled placeholder graphics in
[`templates/placeholders/`](templates/placeholders) so the blank template
previews cleanly:

| Slot      | Placeholder                       | Replace with |
|-----------|-----------------------------------|--------------|
| Hero      | `placeholders/hero.svg`           | hosted hero photo URL |
| Secondary | `placeholders/secondary.svg`      | hosted lifestyle photo URL |
| Grid 1–4  | `placeholders/grid-1.svg` … `grid-4.svg` | hosted interior photo URLs |

Swap each `src` for your hosted photo URL when building an edition. The HTX
**logo** (header), **emblem** (footer), and the **agent contact card** are
already wired to the brand assets / constants in this repo — nothing to
replace.

## What's public vs. local

This repo is public, so it contains only what's needed to view and reproduce a
newsletter — HTML, brand assets, and property photos. Internal material
(recipient lists, drafts, analytics, agent config) is excluded via
[`.gitignore`](.gitignore). Keep private notes in an `_internal/` folder or a
`*.local.md` file and they will not be committed.
