# HTML to JSX Converter

Paste HTML and get valid JSX you can drop into a React component. It renames the attributes React expects, converts inline styles to objects, self-closes void elements, and rewrites comments. The HTML is parsed with the browser's built-in parser and never executed. Runs entirely in your browser, no server, no tracking, no external dependencies.

**Live demo:** https://0xelitesystem.github.io/html-to-jsx-converter/

## Use

1. Paste HTML into the HTML input box, or click **Load example**.
2. Click **Convert to JSX** (output also updates as you type).
3. Review the JSX output, especially anything the limitation note mentions.
4. Click **Copy** and drop the result into your React component.

## Why this exists

Pasting HTML into React means renaming attributes, rewriting inline styles, and closing void tags by hand. This tool does that transform with the browser's own parser and never executes the markup. It is one HTML file with inline CSS and JavaScript: no account, no tracking, no analytics, no external scripts or fonts, and it works offline. MIT licensed, so you can fork it, self-host it, or read every line.

## Features

- Renames `class` to `className` and `for` to `htmlFor`.
- CamelCases the attributes JSX requires, including `tabindex` to `tabIndex`, `readonly` to `readOnly`, `maxlength` to `maxLength`, and hyphenated SVG attributes like `stroke-width` to `strokeWidth`.
- Leaves `data-*` and `aria-*` attributes untouched, since JSX keeps those hyphenated.
- Converts inline `style="color: red; font-size: 12px"` strings into JSX style objects: `style={{ color: 'red', fontSize: '12px' }}`. CSS custom properties (`--foo`) are preserved and quoted.
- Self-closes void elements (`img`, `br`, `input`, `hr`, and the rest).
- Handles boolean attributes: valueless HTML attributes like `disabled` become bare JSX props.
- Converts HTML comments to JSX `{/* ... */}` comments.
- Escapes literal `{` and `}` in text so JSX does not treat them as expressions.
- Wraps multiple top-level elements in a `<>...</>` fragment so the output is a single valid expression.
- Output box with a one-click copy button, plus a load-example button.
- Light and dark themes, keyboard usable, live updates as you type.

Honest limitation, stated in the UI: this is a best-effort static transform. It does not convert `<script>` bodies or inline event-handler strings (`onclick="..."`), and it does not understand template or framework syntax. Review the output before shipping.

## How it works

The HTML is parsed with the browser's `DOMParser` into a real DOM tree. `DOMParser` builds the tree without executing any scripts or event handlers, so pasting untrusted markup is safe. The tool then walks that tree and serializes each node back out as JSX, applying the attribute renames, the style-object conversion, void-element self-closing, and comment rewriting along the way.

## Privacy

Everything runs client-side in your browser. The markup you paste never leaves your machine. There are no network requests, no analytics, and no external dependencies. Check the page source or your browser network tab to confirm. The only thing written to storage is your light or dark theme choice, saved in localStorage under the key `theme`.

## Run locally

```bash
git clone https://github.com/0xelitesystem/html-to-jsx-converter
cd html-to-jsx-converter
```

Then open `index.html` in any modern browser. Or serve the folder with `python -m http.server 8000` and visit http://localhost:8000.

## Build

No build step. The whole tool is one `index.html` with no dependencies, so there is nothing to install or compile.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
