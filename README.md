# Vizara Studio — website + support widget

Static single-page site (React via Babel CDN, Tailwind CDN) for Vizara Studio, including the AI chatbot demo section and the embeddable support widget.

**Live:** https://vizarastudioo.netlify.app

Related backend: https://github.com/Wsif123/vizara-support-agent — full operational docs live in that repo's `HANDOVER.md`.

## Layout

```
index.html          # entire site (markup, styles, React components)
chat-widget.js      # support widget loaded by index.html
assets/             # portfolio images + videos
```

## Widget

`index.html` loads the widget at the end of `<body>`:

```html
<script src="/chat-widget.js"
        data-api-url="https://vizara-support-agent.onrender.com/chat"
        data-client-id="vizara"></script>
```

- `data-api-url` — backend `/chat` endpoint (point at `http://localhost:8000/chat` for local dev)
- `data-client-id` — optional; defaults to `"vizara"`. Sent in every request body.
- `data-brand-name`, `data-greeting`, `data-followup-name`, `data-header-sub` — optional branding overrides for white-label clients.
- Requests carry the browser's `Origin` header automatically; the backend allowlists `vizarastudioo.netlify.app`.

Design: void-black panel, nebula-purple accents, launcher bubble ↔ panel, SVG icons. Text overflow is fixed via `overflow-wrap: break-word` and `word-break: break-word` on message bubbles (`padding: 12px 16px`, `line-height: 1.6`).

The canonical widget shipped to other customers is served by the backend at `/widget/chat-widget.js`; this repo hosts the copy used by the Vizara site. If you change widget behavior, update both (`chat-widget.js` here and `widget/chat-widget.js` in the backend repo).

## Local preview

Just open `index.html` in a browser. Note that the widget script tag points at the **production** backend; switch `data-api-url` to `http://localhost:8000/chat` when testing locally.

## Deploy

Netlify auto-deploys the `main` branch (publish directory = repo root). No build step.
