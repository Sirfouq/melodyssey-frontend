# 🎧 MELODYSSEY

**Describe a mood — get a real, playable Spotify playlist, curated by AI.**

Type something like *"rainy Sunday, slow coding session"* and MELODYSSEY builds a set
of real Spotify tracks and plays them right in the browser. An LLM does the curation;
Spotify provides the catalog and playback.

**▶️ Live:** https://melodyssey.vercel.app

> _Screenshot / demo GIF here (`docs/demo.gif`)._

---

## Why it's built this way

Spotify **deprecated its Recommendations and Audio Features APIs for new apps** (late
2024) — exactly what most "mood playlist" projects depend on. MELODYSSEY sidesteps
that by using an LLM as the recommendation engine and Spotify purely for search and
playback.

## How it works

```
mood ──> Frontend ──POST /api/generate──> Backend ──> OpenAI (curates real tracks)
                                                  └──> Spotify Search (resolves each)
                                                            │
                     playlist rendered + streamed <─────────┘
                     via the Spotify Web Playback SDK
```

Backend (Flask) lives in its own repo — **[melodyssey-backend](https://github.com/Sirfouq/melodyssey-backend)**.

## Features

- 🧠 Natural-language mood → 15–20 real, verified tracks (with optional genre/artist steering)
- ▶️ Full in-browser playback (play/pause/seek/skip/volume) via the Web Playback SDK
- 🔐 Spotify OAuth with secure, `HttpOnly` session cookies

## Tech stack

React 19 · TypeScript · Vite 7 · Tailwind v4 + shadcn/ui · React Router v7 · Spotify Web Playback SDK · deployed on Vercel

## Run locally

```bash
npm install
npm run dev        # http://127.0.0.1:5173
```

Requires the [backend](https://github.com/Sirfouq/melodyssey-backend) running on
`:5000` (Vite proxies `/api/*` to it) and a Spotify **Premium** account for playback.
