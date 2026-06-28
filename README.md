# meridian.

> *time is the only meridian worth crossing*

A celestial focus timer — no frameworks, no build step, no tracking. Just two HTML files and your Google account to sync data across devices.

**Live:** [meridianfocus.vercel.app](https://meridianfocus.vercel.app)

---

## what it is

meridian. is a focus timer built around the metaphor of the sun crossing the sky. A glowing orb travels an arc from east to west as your session progresses, reaching zenith at the halfway point. The interface is dark, typographic, and deliberately minimal — designed to stay out of your way while you work.

All data (stats, tasks, settings) is stored in your browser's `localStorage` and tied to your Google account on the device. Sign in once and your session persists for 7 days.

---

## modes

| # | mode | default timing |
|---|------|----------------|
| 01 | **Pomodoro** | 25 min focus · 5 min short break · 15 min long break · 4 cycles |
| 02 | **Animedoro** | 40 min focus · 20 min break (one anime episode) |
| 03 | **52 / 17** | 52 min focus · 17 min break |
| 04 | **Stopwatch** | counts up indefinitely |
| 05 | **Countdown** | custom duration, counts down |

All timings are fully adjustable from Settings.

---

## features

**Timer**
- Celestial arc dial — orb tracks session progress along a bezier arc from horizon to horizon
- Shimmer ring animation fires when the orb crosses zenith
- Phase accent color shifts from ember (focus) to jade (break)
- Progress scrub bar below the numerals
- Auto-start next phase toggle

**Alarm sounds** (synthesised via Web Audio API, no audio files)
- Deep bell — low sine partials, slow decay
- Soft chime — ascending triad, gentle
- Digital beep — square wave, short
- Rain — filtered white noise
- Electronic pulse — LFO-modulated sine
- Minimal click — triangle wave, curt

**Tasks**
- Add tasks inline during a session
- Check off completed tasks (strikethrough with italic styling)
- Tasks persist across page reloads

**Statistics**
- Total focus time (all time + today)
- Sessions completed (all time + today)
- Breaks taken
- Current streak (consecutive days with at least one session)
- 14-day bar chart history
- Daily goal progress (configurable, default 4 sessions)

**Settings**
- Per-mode timing customisation (focus, break, cycles)
- Auto-start next phase
- 12h / 24h clock toggle
- Daily goal target
- Alarm sound selector with preview

**Keyboard shortcuts**
| key | action |
|-----|--------|
| `Space` | begin / pause |
| `R` | reset |
| `S` | skip phase |
| `1` – `5` | switch mode |

---

## stack

```
meridian/
├── index.html   # landing page + Google sign-in
└── app.html     # the full timer application
```

- **Zero dependencies.** No npm, no bundler, no framework.
- **Vanilla JS** — one self-invoking IIFE, no modules.
- **CSS custom properties** for theming and phase transitions.
- **Web Audio API** for all sounds — synthesised at runtime, no audio files.
- **Google Identity Services (GIS)** for sign-in — JWT decoded client-side for session storage.
- **localStorage** for all persistence (`meridian.v1` key for app data, `meridian.user` for session).
- **Fonts:** Newsreader (serif, display) + IBM Plex Mono (monospace, labels) via Google Fonts.
- **Deployed on Vercel** — static, no server.

---

## auth

Sign-in uses Google Identity Services One Tap. On success, the JWT payload (name, email, picture, sub) is decoded client-side and stored in `localStorage` with a 7-day expiry. No data is sent to any server — there is no backend.

> **Note:** The OAuth consent screen must be in Production mode (not Testing) for any Google account to sign in. See the [Google Cloud Console](https://console.cloud.google.com) → APIs & Services → OAuth consent screen → Publish App.

---

## running locally

Because Google OAuth blocks `file://` origins, you need a local server:

```bash
# with VS Code Live Server — open index.html and click Go Live
# or with Python
python -m http.server 5500
# then open http://127.0.0.1:5500
```

Add `http://127.0.0.1:5500` and `http://localhost:5500` to your OAuth client's **Authorized JavaScript origins** in Google Cloud Console.

---

## design

- **Palette:** `#0B0E13` ink · `#E8E4D8` bone · `#C26A3A` ember · `#5E8581` jade
- **Type scale:** Newsreader 200–300 weight for display; IBM Plex Mono 300–400 for all metadata and labels
- Film grain overlay via inline SVG `feTurbulence` filter
- Ambient radial gradients and a drifting orb on the landing page
- Accent color transitions globally via CSS custom property `--accent` on `body[data-phase]`

---

## license

MIT — do whatever you want with it.

---

*built by [Subhaan Malek](https://hisubhaan.vercel.app)*
