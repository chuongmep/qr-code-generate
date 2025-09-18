# QR Code Generator

Create and download QR codes instantly in your browser — no accounts, no fees, no tracking.

This is a lightweight, single-file web app that uses the excellent `qrcode` library to generate PNG and SVG QR codes with configurable size and error correction level.

## Demo

Open `index.html` directly in your browser and start generating QR codes. Works offline.

## Features

- Generate QR codes from any text or URL
- Choose image size (pixels)
- Select error correction level (`L`, `M`, `Q`, `H`)
- One-click download as PNG
- One-click download as SVG (vector)
- 100% client-side, privacy-friendly, no dependencies to install

## Quick Start

1. Clone this repository
   
	```bash
	git clone https://github.com/chuongmep/qr-code-generate.git
	cd qr-code-generate
	```

2. Open `index.html` in your browser (double-click it or drag it into a browser window).

That's it. You can also serve it locally if you prefer:

```bash
# macOS/Linux with Python 3
python3 -m http.server 8080
# then open http://localhost:8080
```

## Usage

1. Enter the text or URL you want to encode
2. Pick a size and error correction level
3. Click `Generate`
4. Use `Download PNG` or `Download SVG` to save the image

Notes:
- Error correction levels trade capacity for resilience. `H` is most resilient but encodes less data; `L` encodes the most but is least resilient.
- SVG downloads are ideal for print or scalable needs.

## Customization

The app is intentionally simple and contained in a single file: `index.html`.

- UI styles: edit the `<style>` block
- Defaults: update initial values for `#text`, `#size`, and `#eclevel`
- QR options: tweak the `opts` object passed to `QRCode.toDataURL` / `QRCode.toString`

The script loads the QR generator from a CDN:

```html
<script src="https://cdn.jsdelivr.net/npm/qrcode/build/qrcode.min.js"></script>
```

If you need full offline support without CDNs, download the library and reference it locally.

## Development

There is no build step. It is a static HTML page. Recommended workflows:

- Open `index.html` directly, or
- Run a simple static server (see Quick Start) to test changes

### Code Overview

- Input elements: `#text`, `#size`, `#eclevel`
- Generate button: `#generate`
- Download buttons: `#downloadPNG`, `#downloadSVG`
- Render target: `#qrcode`

Core generation snippet:

```js
const opts = { errorCorrectionLevel: ec, width: size, margin: 1 };
lastDataUrl = await QRCode.toDataURL(text, opts);
```

SVG export:

```js
const svg = await QRCode.toString(text, { type: 'svg', errorCorrectionLevel: ec, width: size });
```

## Tech Stack

- Plain HTML/CSS/JavaScript
- [`qrcode` library](https://github.com/soldair/node-qrcode) via CDN

## License

This project is open-sourced under the MIT License. See `LICENSE` for details.

## Acknowledgements

- QR generation powered by the `qrcode` library by soldair and contributors

## Why this exists

Some QR code tools charge for basic features. This project shows how to build a clean, free, offline-capable QR generator with only a few lines of code.

