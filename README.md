# Fractalic

A self-contained **fluted / reeded-glass effect studio** in a single `index.html` — no build step, no dependencies. Drop in any image, tune the glass live, and export the result as a PNG.

![Fractalic](https://img.shields.io/badge/vanilla-HTML%20%2B%20CSS%20%2B%20SVG-111)

## What it does

Recreates the look of vertical fluted glass over a photo:

- **Refraction** — an SVG `feDisplacementMap` driven by a per-reed sawtooth pattern slices the image into ~50 narrow vertical columns, each displaced sideways so subject edges break stepwise column-to-column.
- **Frost** — a light `feGaussianBlur` so only large tonal masses survive.
- **Rib shading** — a `repeating-linear-gradient` (shadow on the left edge of each reed, highlight on the right) blended with `mix-blend-mode: soft-light` to fake the 3D ridges. Its pixel period is kept identical to the displacement wavelength so the ribs line up with the refraction.
- **Film grain** — a tiled monochrome `feTurbulence` noise overlay.

The foreground text/UI sits above the glass layer, so it stays perfectly sharp.

## Controls

| Control | What it changes |
|---|---|
| Rib width | Pixel period of one reed (also rebuilds the SVG displacement map) |
| Refraction | `feDisplacementMap` scale (0–100) |
| Frost / blur | `feGaussianBlur` amount |
| Rib highlight / shadow | Opacity of the ridge gradient |
| Film grain | Grain overlay opacity |
| Grayscale | Mono ↔ colour |
| Show title overlay | Toggle the hero text |
| Download PNG | Re-renders the full pipeline to a canvas and exports at full resolution |

All effect parameters are exposed as CSS custom properties on `:root`
(`--rib-width`, `--refraction-strength`, `--blur`, `--highlight-opacity`,
`--shadow-opacity`, `--grain`) — the sliders just write to them.

## Usage

Open `index.html` in any modern browser. That's it.

Or serve it locally:

```bash
npx serve .
```

Then upload / drop an image, or paste an image URL.

> **Export note:** uploaded files always export. Some remote image URLs block
> canvas export for security (CORS) — upload the file in that case.

## License

MIT
