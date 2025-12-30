# Textarea

A _minimalist_ text editor that lives entirely in your browser and stores everything in the URL hash.

## Features

- 🗜️ **Compression** – Your text gets compressed with Brotli (with deflate fallback)
- 🔗 **URL hash** – Share your notes by copying a URL
- ✨ **Markdown** – Live syntax highlighting via CSS Custom Highlight API
- 💕 **Style** – Customize the look with CSS via DevTools

## Markdown Support

Type markdown and see it styled in real-time:
- **Bold** (`**text**`)
- *Italic* (`*text*`)
- `Code` (`` `code` ``)
- ~~Strikethrough~~ (`~~text~~`)
- Links (`[text](url)`)
- Images (`![alt](url)`)
- Headings (`# H1` through `###### H6`)
- Code blocks (triple backticks)
- Blockquotes (`> text`)
- Horizontal rules (`---`)
- Lists (`- item`, `1. item`)
- Task lists (`- [ ] todo`, `- [x] done`)

Markdown syntax markers are dimmed for a clean reading experience.

## Pro tips

- Start your document with `# Title` to set a custom page title
- Your data lives in localStorage AND the URL
- Add a `style` attribute to the `<article>` tag via DevTools. It'll be saved in the URL too!
- Add `/qr` to the URL to get a QR code for the current page

---

*Made with ❤️ and JavaScript*
