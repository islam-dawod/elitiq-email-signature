# Elitiq Group — Email Signature Handoff (Final)
Ibrahim Odeh · Operations Manager · 3 variants · 600 × 200 px

## What's inside
```
01-pill-strokes.html   02-color-blocks.html   03-noir.html
images/     all assets, exported @2x (displayed at 1x via width/height attributes)
previews/   pixel-reference renders of each signature @2x (1200 × 400)
index.html  opens all three previews side by side
```
Each HTML file is already email-safe: table layout, inline CSS only, no flex/grid/position, no JS, no base64.
The signature itself is between the `SIGNATURE START` / `SIGNATURE END` comments.

## Setup (3 steps)
1. **Upload `images/` to a public HTTPS location** (company CDN, website `/assets/email/`, S3…).
2. **Find & replace** `src="images/` → `src="https://YOUR-HOST/path/` in the chosen HTML file.
   Absolute URLs are required — relative paths and base64 are stripped by Gmail/Outlook.
3. Open the file in Chrome, select the signature, copy, paste into the client's signature settings
   (Gmail: Settings › Signature · Outlook: Settings › Mail › Signatures · Apple Mail: paste, then untick "Always match my default message font").

## Specs
| Token | Value |
|---|---|
| Ink (text, logo) | `#0A0A0C` |
| Mint | `#C8F8EA` |
| Pink | `#FCD6FB` |
| Blue | `#D3E2FD` |
| Body grey (on white) | `#3F3F46` · on Noir `#D4D4D8` |
| Divider (white / noir) | `#E4E4E7` / `#2E2E33` |
| Font | Urbanist 300 / 500 / 800 — fallback `'Helvetica Neue', Helvetica, Arial, sans-serif` |
| Name | 27 px (01, 03) · 32 px uppercase, 2 lines (02) — "Ibrahim" 800, "Odeh" 300 |
| Email | 12.5 px, 500, `mailto:` link, no underline |
| Title chip | **image** (`chip-light.png` / `chip-dark.png`): mint → white → pink gradient at 100°, inner highlight, soft shadow; text 9.5 px, 700, tracking 0.2em |
| Logo widths | 138 (01) · 92 (02) · 128 white (03) |

**Note on the chip:** it's an image on purpose — gradients, inner highlights and shadows don't render in Outlook/Gmail.
Each chip PNG includes a 10 px bleed around it for the shadow; the layout already compensates (the text rows have `padding-left:10px`), so don't trim the images.
To make a signature for another employee, the title chip must be re-exported with the new title.

## Known client behaviour (expected, not bugs)
- **Urbanist** loads in Apple Mail / iOS Mail. Gmail & Outlook fall back to Helvetica/Arial — layout is sized to survive it.
- All shapes (pills, blocks, circles, chip) are images, so they render the same everywhere, including Outlook desktop.
- **Dark mode**: `03-noir` is the safest. White variants may get their background darkened by Gmail/Outlook apps while images keep their white fill — test before rolling out.
- Keep the total width at **600 px**; don't scale images in CSS.

## QA checklist
Gmail web · Gmail iOS/Android · Outlook 365 web · Outlook desktop (Windows) · Apple Mail macOS/iOS — check the email link is clickable and images load after a real send (not just in compose).
