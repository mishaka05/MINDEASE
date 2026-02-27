# 🐻 MindEase — AI Mental Health Companion

> A browser-based AI mental health companion for students — empathetic chat, mood tracking, therapy discovery, and self-help resources. Built as a single HTML file with full OWASP security hardening.

---

## 📸 Preview

| Dark Mode | Light Mode |
|---|---|
| Deep warm charcoal aesthetic | Warm parchment botanical aesthetic |

---

## ✨ Features

- **💬 AI Chat** — Claude-powered empathetic conversations with real-time mood detection, wellness tips, and automatic crisis resource surfacing
- **📊 Mood Tracker** — Daily emoji check-ins, weekly bar chart, streak counter, and mood trend history
- **🏥 Therapy Finder** — Searchable, filterable directory of affordable therapists with built-in booking modal
- **📚 Self-Help Resources** — Curated cards covering anxiety, stress, sleep, and mindfulness
- **🌙 Light / Dark Mode** — Full theme system with persistent toggle, inspired by botanical warm and moody monochrome aesthetics
- **🆘 Crisis Detection** — Auto-detects distress keywords and surfaces Indian helplines (iCall, Vandrevala, NIMHANS)
- **📱 Fully Responsive** — Works on mobile, tablet, and desktop

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5 + CSS3 + Vanilla JS (ES2020) |
| AI Engine | Anthropic Claude API |
| Typography | DM Sans, DM Serif Display, Fraunces (Google Fonts) |
| Security | CSP sha256, Rate Limiter, InputValidator, DOM factory |
| Deployment | Any static host — GitHub Pages, Netlify, Vercel |

---

## 🚀 Getting Started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/mindease.git
cd mindease
```

### 2. Open directly (demo mode)

```bash
open mental-health-companion-secure.html
```

> In demo mode the app uses the Claude.ai sandbox proxy automatically — no API key needed to test the UI.

### 3. Production setup

Create a backend proxy endpoint (e.g. `/api/chat`) that attaches your API key server-side:

```js
// Example: Express.js proxy
app.post('/api/chat', async (req, res) => {
  const response = await fetch('https://api.anthropic.com/v1/messages', {
    method: 'POST',
    headers: {
      'x-api-key': process.env.ANTHROPIC_API_KEY,
      'anthropic-version': '2023-06-01',
      'content-type': 'application/json'
    },
    body: JSON.stringify(req.body)
  });
  res.json(await response.json());
});
```

Then update `CONFIG.API_PROXY_URL` in the HTML file to point to your endpoint.

> ⚠️ **Never** hardcode the API key in the HTML file. Always use environment variables.

---

## 🔐 Security Architecture

All OWASP Top 10 mitigations are implemented and locked:

| Control | OWASP Ref | Implementation |
|---|---|---|
| API Key Protection | A02 | Server-side only, never in client code |
| Content Security Policy | A05 | sha256 hash verified on every script edit |
| Rate Limiting | A04 | Token bucket — 20 msg/60s, fail-closed |
| Input Validation | A03 | `InputValidator` schemas on all inputs |
| XSS Prevention | A03 | `el()` DOM factory — zero `innerHTML` with user data |
| Prompt Injection | A03 | `PROMPT_LABEL_ALLOWLIST` + `sanitizeForPrompt()` |

> The security module is **read-only**. Any UI changes must not touch the security block.

---

## 📁 Project Structure

```
mindease/
├── mental-health-companion-secure.html   # Main app (single file)
├── README.md                             # This file
├── .gitignore                            # Ignores env files, OS junk
└── assets/                               # (optional) screenshots
    ├── screenshot-dark.png
    └── screenshot-light.png
```

---

## 🧠 Algorithm Flow

```
User message
    │
    ▼
InputValidator.validate()        ← sanitise + length check
    │
    ▼
sanitizeForPrompt()              ← strip injection attempts
    │
    ▼
RateLimiter.consume('chat')      ← token bucket (20 msg / 60s)
    │
    ▼
Anthropic Claude API (proxied)   ← system prompt + chat history
    │
    ▼
Parse response
    ├── moodTag      → sentiment chip
    ├── wellnessTip  → tip card
    ├── crisisFlag   → red alert + helplines
    └── message text → safe DOM via el() factory
```

---

## 📊 Results

- ✅ 28/31 OWASP automated checks passed
- ✅ `node --check` passes with zero errors
- ✅ WCAG AA contrast on all primary text combinations
- ✅ Single file ~130 KB — FCP < 1.5s on 3G
- ✅ Fully responsive — mobile, tablet, desktop

---

## 🔭 Future Scope

- 📱 React Native mobile app with push notifications
- 🌐 Hindi, Tamil, Telugu localisation
- 🔐 User accounts with persistent mood history
- 📈 Anonymised campus mental health analytics dashboard
- 🤝 Verified therapist portal with video consultation

---

## 📚 References

- [Anthropic Claude API](https://docs.anthropic.com)
- [OWASP Top 10](https://owasp.org/Top10)
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21)
- [iCall Helpline (TISS)](https://icallhelpline.org) — 9152987821
- [Vandrevala Foundation](https://www.vandrevalafoundation.com) — 1860-2662-345
- [NIMHANS](https://nimhans.ac.in)

---

## 👩‍💻 Presented By

**M NANTHINI** · XYZ College · Department of Computer Science & Engineering · 2026

---

*Built with care for student mental health 🐻*
