# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Textarea is a minimalist browser-based text editor that stores everything in the URL hash. No backend—all state persists via Brotli-compressed data in the URL fragment and localStorage.

## Architecture

**Single-file application**: The entire app lives in `index.html` with inline CSS and JavaScript. No build system, no dependencies, no bundler.

**Data flow**:
- Text content + optional `<article>` style attribute → compressed with Brotli (fallback: deflate-raw) → base64url encoded → stored in URL hash
- Format prefix: `0` = deflate-raw, `1` = Brotli (for backwards compatibility with legacy unprefixed deflate)
- Separator: `\x00` between content and style attribute

**Markdown highlighting**: Uses CSS Custom Highlight API (`::highlight()`) for live syntax highlighting. Only `color`, `background-color`, and `text-decoration` are supported—no font properties. Feature-detected via `'highlights' in CSS`.

Supported patterns:
- **Inline**: bold (`**`), italic (`*`), code (`` ` ``), strikethrough (`~~`), links (`[text](url)`), images (`![alt](url)`)
- **Block**: headings (`#`), code blocks (`` ``` ``), blockquotes (`>`), horizontal rules (`---`), lists (`-`, `*`, `+`, `1.`), task lists (`- [ ]`, `- [x]`)

**Key functions in index.html**:
- `compress()` / `decompress()` - URL hash encoding/decoding
- `highlightMarkdown()` - Parses text and creates Range objects for CSS highlights
- `save()` / `load()` - Sync between URL hash, localStorage, and DOM
- `download()` - Export as standalone HTML file (Ctrl/Cmd+S)

**Service worker** (`sw.js`): Caches `/` and `/qr` for offline PWA support. Bump `CACHE_NAME` version when updating.

**QR page** (`qr.html`): Generates QR code SVG for the current URL. Uses embedded minified qrcode library.

## Development

Serve locally with any static server:
```bash
python -m http.server 8000
# or
npx serve .
```

No build step, tests, or linting configured—edit files directly and refresh browser.

## Key Constraints

- `contenteditable="plaintext-only"` on `<article>` means browser handles line breaks as `<br>` elements
- Markdown highlighter must account for `<br>` elements contributing newlines (see `walkNodes()` and `nodePositions` array)
- CSS Highlight API ranges cannot span across element boundaries cleanly—ranges must be recalculated on every input
