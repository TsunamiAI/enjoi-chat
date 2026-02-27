# ENJOi Copy Assistant — Chat Frontend

A single-page web app that wraps the n8n `@n8n/chat` widget with a conversation history sidebar. Provides a ChatGPT-like experience for the ENJOi brand copy assistant.

## Features

- Login with Basic Auth (credentials validated against the n8n webhook)
- Conversation sidebar with session history
- New Chat button creates fresh sessions
- Click a past session to reload its messages
- ENJOi brand colours and Raleway typography
- Responsive layout — sidebar collapses on mobile

## Files

```
enjoi-chat/
  index.html    Single-page app (HTML + inline CSS + JS)
  README.md     This file
  .gitignore
```

## Configuration

The two webhook URLs are defined at the top of the `<script>` block in `index.html`:

| Variable | Purpose |
|----------|---------|
| `WEBHOOK_URL` | n8n Chat Trigger webhook (handles messages and session loading) |
| `SESSIONS_URL` | n8n webhook that returns the session list as JSON |

To change them, edit the constants in `index.html`:

```js
const WEBHOOK_URL = 'https://belucent.app.n8n.cloud/webhook/...';
const SESSIONS_URL = 'https://belucent.app.n8n.cloud/webhook/enjoi-sessions';
```

## Sessions endpoint

The `SESSIONS_URL` endpoint should return a JSON array:

```json
[
  {
    "sessionId": "uuid-string",
    "title": "First message or summary",
    "date": "2026-02-27T10:30:00Z"
  }
]
```

## Deploy to Vercel

1. Push this folder to a GitHub repo (or use the Vercel CLI).
2. In Vercel, create a new project and point it at the repo.
3. **Framework Preset**: select "Other" (static site).
4. **Root Directory**: set to `enjoi-chat` (or wherever the `index.html` lives).
5. Deploy. Vercel will serve `index.html` as a static site.

No build step, no dependencies, no `package.json` needed.

## Local development

Open `index.html` directly in a browser, or serve it locally:

```bash
npx serve enjoi-chat
```

## Tech stack

- Vanilla HTML/CSS/JS (no framework, no build tools)
- [`@n8n/chat`](https://www.npmjs.com/package/@n8n/chat) widget via CDN
- [Raleway](https://fonts.google.com/specimen/Raleway) from Google Fonts
