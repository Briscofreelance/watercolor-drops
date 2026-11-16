# Watercolor Drops

A tweakable WebGL hero: bleeding watercolor drops on paper, rendered by one fragment shader. Change the palette, drop size, spread, edge roughness, granulation and paper in real time, then export the result as **one self-contained HTML file** (no library, no image).

**Live demo:** https://codepen.io/Briscofreelance/pen/01a1e650-eb02-730f-b07e-506097474235

## Use

Open `index.html` (or the live demo). Adjust the settings in the panel, then:

- **Copy HTML / Download .html**: a standalone page with your settings baked in.
- **Save PNG**: a still on your paper color.
- **Copy settings**: the settings as JSON.
- **Copy link**: the address carries every setting, so a look can be shared as a URL.

Shortcut: `H` hides or shows the panel. Click the canvas to add a drop.

## How it works

- Drops fall, then spread: radius follows `1 - exp(-age * k)`, fast at first, then slower, like wet paint.
- The edge is distorted with fractal noise plus random lobes, so no two drops look the same.
- Each pigment is a *transmittance* color. Layers multiply (`col *= pow(rgb, alpha)`): a subtractive mix, so yellow over blue turns green.
- Pigment migrates to the edge, granulates on the paper grain and thins as it spreads.
- Performance: ~30 fps cap, reduced render resolution, paused when off-screen or hidden, static composition when `prefers-reduced-motion` is set or no GPU is available.

The whole engine is a single function, `createWatercolor(canvas, hero, options)`. The export copies its source as-is.

## License

MIT, see `LICENSE`.
