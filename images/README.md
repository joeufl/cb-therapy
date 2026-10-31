# Images

All files here came off the old Wix site. **They were saved with `.jpg` and `.png`
extensions but were actually AVIF files** — that's what Wix's `enc_avif` export
produces. They have been converted to real JPEG and PNG. If you pull more images
from Wix, check the format before committing:

```sh
file images/*        # should say "JPEG image data" / "PNG image data", never "AVIF"
```

An AVIF file named `.jpg` mostly renders in modern browsers, but it breaks link-preview
crawlers (WhatsApp, LinkedIn, iMessage) and older Safari — and an AVIF favicon does not
render at all.

## In use

| File | Size | Used for |
|---|---|---|
| `catherine-bush.jpg` | 546 × 748 | Portrait in the About section, both languages |
| `couch.jpg` | 546 × 1120 | Practice photo beside the Welcome text |
| `first_interview_icon.jpg` | 121 × 121 | Round icon, First Interview card |
| `individual_therapy.jpg` | 121 × 121 | Round icon, Individual Therapy card |
| `couple_therapy_icon.jpg` | 121 × 121 | Round icon, Couple & Family card |
| `favicon.png` | 64 × 64 | Browser tab icon (transparent) |
| `apple-touch-icon.png` | 180 × 180 | Home-screen icon (flattened onto cream — iOS renders transparency as black) |
| `og-image.jpg` | 1200 × 630 | Link preview when the site is shared |

The three card icons are only 121px wide, which is why they display at 60px — large
enough to stay crisp on a 2× screen, and they will look soft if scaled up. If better
versions exist, drop them in at 240 × 240 or larger.

`favicon.png`, `apple-touch-icon.png` and `og-image.jpg` were generated from the
original 1254 × 1254 CB monogram, pulled from Wix at full resolution. The one on the
old site was only 39 × 39.

## Not currently used

| File | Size | Note |
|---|---|---|
| `catherine-bush-standing.jpg` | 340 × 513 | A second portrait, same session and outfit as the seated one. Left out because two near-identical portraits add little, and at 340px it's too small for a hero image. Easy to swap in if preferred. |

## If you replace anything

Keep the filenames — the HTML references them by path, and the portrait and practice
photo have `width`/`height` attributes that should be updated to match any new file's
real dimensions. Export as JPEG at ~85–90% quality. The portrait wants roughly a 4:5
crop; the practice photo is a tall 1:2 crop on desktop and is re-cropped to 3:2 on
phones via `object-fit`.
