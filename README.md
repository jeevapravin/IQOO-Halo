# Halo Simulator

**An interactive prototype demonstrating the Halo ambient notification ring — an AI-powered context-aware notification system for iQOO devices.**

> Software simulation of the Halo ring output — production version drives the physical Monster Halo LED ring on iQOO devices, classifying notifications with a small on-device model instead of a cloud API.

![Halo Simulator Demo](screenshot.png)

---

## Overview

The Halo Simulator is a single-page web application that demonstrates how an ambient LED notification ring on a smartphone can intelligently communicate notification urgency through **color**, **glow intensity**, and **pulse rhythm** — driven by a context-aware AI fusion engine.

### Ring States

| State | Color | Pulse | Trigger |
|-------|-------|-------|---------|
| **Calm** | 🔵 Blue | Slow 3s breathing | No pending notifications or only low-priority |
| **Building** | 🟠 Amber | Steady 1.5s pulse | 3+ low-priority notifications accumulated |
| **Urgent** | 🟠 Amber | Fast 0.8s pulse | High-priority notification pending |
| **Critical** | 🔴 Red | Sharp 0.3s triple-burst | High-priority notification while in a meeting |

### Context Modifiers

- **Focus Mode**: Suppresses escalation for anything below high-priority
- **Ambient Noise**: High noise environments bias toward suppressing amber "building" states
- **Meeting Status**: Triggers critical escalation when combined with high-priority notifications

---

## Getting Started

### Quick Start

1. Clone this repository
2. Open `index.html` in any modern browser (Chrome, Firefox, Edge, Safari)
3. That's it — no build step, no server, no dependencies to install

```bash
git clone <your-repo-url>
cd IQOO
open index.html   # macOS
# or
xdg-open index.html   # Linux
# or just double-click the file
```

### Live Classification (Optional)

The app includes a **Live Classification** feature that uses the Gemini API to classify messages by semantic urgency (not simple keyword matching).

To enable it:

1. Get a free API key from [Google AI Studio](https://aistudio.google.com/)
2. Open `index.html` in a text editor
3. Find the line near the top of the `<script>` section:
   ```javascript
   const GEMINI_API_KEY = "PASTE_KEY_HERE";
   ```
4. Replace `PASTE_KEY_HERE` with your actual API key
5. Refresh the page

> ⚠️ **Security Note**: The API key is stored in plaintext in the HTML file. This is acceptable for local demo use only. **Do not commit a real API key to a public repository.**

Without an API key, the Live Classification falls back to a local rule-based classifier that still works well for common urgent patterns.

---

## Tech Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| HTML5 | — | Structure |
| [Tailwind CSS](https://tailwindcss.com/) | v4 (CDN) | Design system, spacing, typography |
| [GSAP](https://gsap.com/) | 3.15.0 (CDN) | Premium animations, smooth state transitions |
| [Google Fonts](https://fonts.google.com/) | — | Inter + Space Grotesk |
| [Gemini API](https://ai.google.dev/) | 3.5 Flash-Lite | Live message classification (optional) |

Everything loads via CDN — **zero build step, zero `npm install`**, just a single HTML file.

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                   User Interface                     │
│  ┌──────────┐  ┌──────────────────────────────────┐ │
│  │  Phone   │  │        Control Panel              │ │
│  │  + Ring  │  │  Buttons / Toggles / Slider       │ │
│  │  + Glow  │  │  Message Input + Send             │ │
│  └──────────┘  └──────────────────────────────────┘ │
│  ┌──────────┐  ┌──────────────────────────────────┐ │
│  │ Reasoning│  │        Event Timeline             │ │
│  └──────────┘  └──────────────────────────────────┘ │
└─────────────────────────┬───────────────────────────┘
                          │
              ┌───────────▼───────────┐
              │    Fusion Logic       │
              │  (Context Engine)     │
              │                       │
              │  Inputs:              │
              │  • Notifications[]    │
              │  • Meeting status     │
              │  • Focus mode         │
              │  • Noise level        │
              │                       │
              │  Output:              │
              │  • Ring state         │
              │  • Reasoning text     │
              └───────────────────────┘
                          │
              ┌───────────▼───────────┐
              │  Classification       │
              │  Pipeline             │
              │                       │
              │  Gemini 3.5 Flash-Lite│
              │     ↓ fallback        │
              │  Gemini 2.0 Flash     │
              │     ↓ fallback        │
              │  Local Classifier     │
              └───────────────────────┘
```

---

## Screen Recording Tips

This prototype is designed to be screen-recorded at **1280×720 or larger**:

- No page scrolling required — everything is visible at once
- All state transitions use smooth GSAP animations (no jarring cuts)
- The ring glow is multi-layered for camera visibility
- The reasoning panel explains every state change in plain language
- The event timeline lets viewers follow the sequence of actions

---

## License

[MIT](LICENSE)

---

## Team

*Add your team members here*
