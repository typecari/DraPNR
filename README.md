# Paula Natalia Rodríguez — sitio y tarjeta digital

This is a plain HTML/CSS/JS site — no build step, no framework, no
tools to install. Open a file in a text editor, save it, push to
GitHub, and the live site updates itself within a minute or two.

## What's live where

| File | Live at | What it is |
|---|---|---|
| `index.html` | `https://TU-DOMINIO/` | The one-page site (hero, services, testimonials, contact) |
| `DRAPNR/index.html` | `https://TU-DOMINIO/DRAPNR` | The digital business card (what the QR code points to) |
| `assets/paula-rodriguez.vcf` | — | Contact file the "Guardar contacto" button on the main site downloads |
| `DRAPNR/assets/paula-rodriguez.vcf` | — | Same, for the "Guardar contacto" button on the card |
| `images/` | — | Every photo/logo/QR used by both pages |

Deployment is automatic: `.github/workflows/static.yml` republishes
the whole repo to GitHub Pages every time you push to `main`. You
don't need to run anything — just save and push.

## Editing text (both languages)

Every piece of translated copy on `index.html` is written **twice**,
wrapped in two small tags right next to each other:

```html
<span class="es">Contactar ahora</span><span class="en">Contact now</span>
```

Only one shows at a time — a class on `<body>` (`lang-es` or
`lang-en`) decides which, and the button in the header flips it.
**To change a word or a sentence: find it in the file, edit the text
inside the matching `<span class="es">` or `<span class="en">`.**
That's the whole system — there's no separate English file to keep
in sync, and nothing else needs to change.

The digital card (`DRAPNR/index.html`) is Spanish-only by design —
it's a physical/QR hand-out, not a page people browse in two
languages — so it has no `es`/`en` spans at all; just edit the text
directly.

> **Note if you also have the older `Paula Rodriguez.dc.html`
> file lying around:** that was a different, builder-tool version of
> this same site (it used `hideEs`/`hideEn` spans and a translation
> script instead of the `es`/`en` classes above). It's no longer
> connected to what's live — **`index.html` and `DRAPNR/index.html`
> are the only files GitHub Pages actually serves.** Editing the old
> `.dc.html` file does nothing to the live site.

## Changing the WhatsApp number / phone

The WhatsApp number appears several times as a link, in this shape:

```
https://wa.me/573155529877?text=...
```

Find-and-replace `573155529877` with the new number (country code, no
`+`, no spaces) everywhere it appears in `index.html`. It's used in:
the header button, the hero's two buttons, the services CTA, and the
contact section.

To change the phone/details someone saves to their phone when they
tap "Guardar contacto," edit the actual contact file, in **both**
places it exists:
- `assets/paula-rodriguez.vcf`
- `DRAPNR/assets/paula-rodriguez.vcf`

It's plain text — open it in any text editor. The format is:

```
BEGIN:VCARD
VERSION:3.0
FN:Paula Natalia Rodríguez
TEL:+573155529877
...
END:VCARD
```

## Changing images

Everything lives in `images/` (site-wide) and `DRAPNR/images/` (card
only). To swap a photo: replace the file (keep the same filename, or
update the `src="images/…"` reference if you rename it). Currently
used:

- `portrait.png` — the hero photo on the main site and the card
- `qr-code.png` — the QR code (points to the `/DRAPNR` page — if you
  ever change the domain, regenerate this)
- `logo-uis-black.png` / `logo-uis-white.png` — university credential mark
- The "About" section has three placeholder photo boxes (clinic
  session / manual therapy / exercise) with no real photos yet —
  see `<!-- No real clinic photos yet -->` in `index.html` to swap
  them in when you have them.

## Testing changes before you push

No server needed — just open the file directly:

- **Mac:** right-click `index.html` → Open With → your browser
- **Windows:** double-click `index.html`

Resize the browser window (or open dev tools' device toolbar,
`Cmd/Ctrl+Shift+M`) to check the mobile layout before pushing.

## The mobile fix (for context)

The previous version of this site had two hero-section elements
(the text block and the portrait) with **hardcoded pixel
dimensions** — they didn't shrink on a narrow screen, so they got
clipped by the page's `overflow-x:hidden`. The current `index.html`
has no fixed pixel widths anywhere in the layout — everything uses
percentages, `flex`, or CSS `grid`, so there's nothing left to clip.
The scroll-parallax effect on the hero photo is also now skipped
entirely on screens ≤760px wide and for anyone with "reduce motion"
turned on, instead of running unconditionally.

## Code comments

Both `index.html` and `DRAPNR/index.html` are organized into
numbered, commented sections right in the `<style>` block (§1
Variables, §2 Base, §3 Language toggle, etc.) — search for `═══` to
jump between them. The `<script>` block at the bottom of `index.html`
is split the same way: language toggle, scroll-reveal, testimonial
rotator, then the hero parallax.
