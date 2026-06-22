# 🎤 Spiel — AI Speech Topic Generator

A speech practice app that generates real-world discussion topics powered by the Anthropic Claude API. Built entirely in vanilla HTML, CSS, and JavaScript — no framework, no backend, no build step.

🔗 **Live Demo:** [spiel-voice.vercel.app](https://spiel-voice.vercel.app)

---

## What It Does

You pick a category and difficulty, hit Generate, and Claude instantly gives you a fresh, real-world topic to practice speaking on — complete with specific angles to cover, data points to mention, and examples to use. If the API is unavailable, it silently falls back to a local bank of 80+ hand-curated topics so the app never feels broken.

---

## Features

- 🤖 **AI-powered topics** — Claude generates unique, context-aware prompts on demand
- 🎯 **8 categories** — GD Round, Current Affairs, Abstract, Social Issues, Motivational, Tech, Career, India Focus
- ⚡ **Easy / Hard difficulty** — filters both AI-generated and local bank topics
- 🔁 **Smart fallback** — local topic bank kicks in silently if the API times out
- ⏱️ **Practice timer** — 1/2/3/5/10 min presets with a full-screen overlay mode
- 📊 **Session tracking** — topic count, streak, and completed sessions
- 📋 **Topic history** — last 6 topics shown, click any to reload
- 📤 **Copy & Share** — copy to clipboard or share via native OS share sheet
- 🌙 **Dark / Light mode** — theme toggle
- 📱 **Fully responsive** — works on mobile and desktop

---

## Tech Stack

- HTML5
- CSS3 (custom animations in `animations.css`)
- Vanilla JavaScript (zero dependencies)
- Anthropic Claude API (`claude-sonnet-4-20250514`)

---

## How the AI Generation Works

1. User clicks Generate
2. App sends a structured prompt to the Anthropic Claude API requesting one topic as a strict JSON object: `{ topic, category, difficulty, hint }`
3. Response is parsed and rendered directly to the DOM
4. An 8-second `AbortController` timeout ensures the app never hangs — if the API doesn't respond in time, it falls back to the local topic bank automatically

```javascript
const res = await fetch("https://api.anthropic.com/v1/messages", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  signal: controller.signal,
  body: JSON.stringify({
    model: "claude-sonnet-4-20250514",
    max_tokens: 300,
    messages: [{ role: "user", content: prompt }]
  })
});
```

> ⚠️ **Note on API key:** The API is currently called client-side for simplicity. The production-grade approach would proxy requests through a small backend so the key never touches the browser. This is a known tradeoff made deliberately for this portfolio project.

---

## Project Structure

```
spiel/
├── index.html        # Entire app — structure, logic, topic bank, API call
├── styles.css        # Layout, components, dark/light themes
└── animations.css    # Entrance animations, transitions, timer effects
```

---

## Local Topic Bank

The app ships with 80+ hand-written topics across all 8 categories, each with a difficulty rating (1–3) and a contextual hint. Topics are de-duplicated using a `Set` of already-shown indices — so you never get the same topic twice until you've cycled through the entire pool.

---

## Getting Started

```bash
git clone https://github.com/Maithilicok/Spiel-Voice.git
cd Spiel-Voice
```

Open `index.html` in any browser. That's it — no install, no build step.

---

## Future Enhancements

- 🔐 Backend proxy for secure API key handling
- 🎙️ Speech-to-text — record your response and get AI feedback
- 📊 Per-topic analytics — track which categories you practice most
- 💾 Save favourite topics across sessions (localStorage)

---

## License

MIT
