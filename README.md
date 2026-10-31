# catherinebush.at

Static site for Catherine Bush Psychotherapy — a psychotherapy practice in Vienna
offering sessions in English and German. Replaces a Wix site.

## Stack

Six static HTML pages sharing one stylesheet. No build step, no dependencies,
no framework. GitHub Pages serves the files directly.

```
index.html            EN home — hero, welcome, services, about, credentials, booking, contact
imprint.html          EN Impressum (legally required in Austria)
privacy.html          EN GDPR privacy policy
de/index.html         DE home
de/impressum.html     DE Impressum
de/datenschutz.html   DE Datenschutzerklärung
style.css             shared stylesheet
images/               portrait, favicon, link-preview image — see images/README.md
TODO.md               next steps, and notes on what was built and why
```

## Languages

`EN | DE` sits in the sticky nav on every page. Each page links to its counterpart
two ways:

- **`hreflang` tags** with absolute URLs — what search engines read.
- **`data-alt-en` / `data-alt-de` on the root element** with relative paths — what the
  language script reads. Keeping these relative is what lets local preview work without
  bouncing to the live domain.

A short inline script in each `<head>` picks the language on first visit:
an explicit choice from the switcher is remembered in `localStorage` (`cb-lang`) and
always wins; otherwise `navigator.language` decides. It runs before render so there's
no flash of the wrong language, and it no-ops safely if storage is blocked. With
JavaScript off, both languages are still fully reachable via the switcher.

**When adding a page, it needs both languages**, plus the `hreflang` tags, the
`data-alt-*` attribute, and the switcher block pointing at its counterpart.

## Local preview

```sh
python3 -m http.server 8000
# → http://localhost:8000
```

Opening `index.html` directly works too, but the server matches production paths.
To test language detection, change your browser's preferred language, or clear
`localStorage` for the origin to reset a remembered choice.

## Deploy

Push to `main`. GitHub Pages rebuilds on push
(Settings → Pages → Deploy from branch → `main` / root).

**Before the first push,** read [TODO.md](TODO.md) § 1. Both privacy policies still
describe Wix as the host, and the German one is missing two sections — neither should
go live as-is. Also delete `test.html` and `testde.html`, the saved Wix pages, which
would otherwise be served publicly.

## Editing

Content is plain HTML in the page files. On the home pages the sections are
`#therapy` / `#angebot`, `#about` / `#ueber-mich`, `#credentials` / `#qualifikation`,
`#schedule` / `#termin`, and `#contact` / `#kontakt`.

Colors and type are CSS custom properties in the `:root` block at the top of
`style.css` — changing `--sage` and `--cream` re-themes the whole site.

The TheraPsy booking calendar is stubbed out in the booking section of both home
pages; the iframe is commented in place with instructions.
