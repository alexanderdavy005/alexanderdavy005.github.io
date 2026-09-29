# Alexander Davydovych — Mechanical Engineering Portfolio

A static, single-page portfolio site built from the source PDF portfolio. No build step, no
package manager, no framework — three files and a folder of images. The only external request is
to Google Fonts for the two typefaces; everything else is served from this repository, and the
font stacks fall back to system fonts if that request fails or is blocked.

**Live site:** _add the GitHub Pages URL here once Pages is enabled_

## Contents

| Path | What it is |
|---|---|
| `index.html` | The entire page — masthead, sticky project nav, 8 project sections, footer, lightbox |
| `styles.css` | All styling, including the light/dark palettes and responsive breakpoints |
| `images/` | 24 project photos and CAD renders extracted from the PDF, plus 4 organisation logos |

## The eight projects

1. **Biomimetic Assistive Glove** — The Biomimetic Wearable Robotics Lab
2. **Exoskeleton Linkage Connector** — The Biomimetic Wearable Robotics Lab
3. **Foot-Pressure Sensor Sole** — The Biomimetic Wearable Robotics Lab
4. **Carbon Capture Filtration Chamber** — CarbonCLAIR
5. **Fuselage Manufacturing** — AIAA
6. **Landing Gear Shock Isolation Pad** — AIAA
7. **Motor Grain Test Stand** — Harlem Launch Alliance
8. **TPU Banner Prototype** — AIAA

Each section keeps the PDF's **What / How / Results** structure. Where the PDF stated concrete
numbers, they are also pulled out into a metrics strip above the prose so they are visible at a
glance.

## Publishing to GitHub Pages

1. Push this repository to GitHub (the repo must be public, or you need a paid plan for private Pages).
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`.
4. Choose branch `main` and folder `/ (root)`, then **Save**.
5. Wait a minute or two. The site appears at `https://<username>.github.io/<repo-name>/`.

To publish at `https://<username>.github.io/` instead of a subpath, name the repository
`<username>.github.io`.

**One thing to edit after the site is live:** the two `og:` meta tags near the top of `index.html`
contain `USER` and `REPO` placeholders. Social link previews (LinkedIn, Slack) require absolute
URLs, so fill in the real Pages address or the preview image will not load.

All asset paths are relative, so the site works correctly at either a root or a subpath URL.

## Working on it locally

Any static file server works. With Python installed:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000`. Opening `index.html` directly via `file://` also works, though
some browsers restrict a few things over that protocol.

## Notes on how it is built

- **No JavaScript needed to read the page.** The only script is the image lightbox; with JS
  disabled every project, image, and line of text is still there.
- **Light and dark.** The palette is defined as CSS custom properties on `:root` and swapped under
  `prefers-color-scheme: dark`, so the page follows the visitor's system theme.
- **Responsive.** Three-up galleries and three-column What/How/Results collapse to two columns
  below 860 px and to one column below 680 px.
- **Accessibility.** Every project image has a descriptive `alt`; gallery images are keyboard
  focusable and open the lightbox on Enter or Space; Escape closes it and focus returns to the
  image; there is a skip link; the page respects `prefers-reduced-motion`.
- **Fonts** are Fraunces (headings) and Inter (body), loaded from Google Fonts with system-font
  fallbacks, so the page still renders sensibly offline. To remove that third-party request
  entirely, delete the three `<link>` tags for Google Fonts in `index.html` — the page then uses
  Georgia and the system UI font.
- **Images** were extracted from the PDF, capped at 1100 px wide and re-encoded — roughly 1.8 MB
  total for all 28 files. CAD renders and diagrams are shown with `object-fit: contain` so no
  geometry is cropped; photographs use `cover`.

## Updating content

Everything is plain HTML. To add a project, copy an existing `<article class="project">` block,
give it a new `id`, drop the images into `images/`, and add a matching link to the `.tocbar` list
near the top of `index.html`.
