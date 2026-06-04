# Deutsch lernen — B1 & B2 Übungen

A self-contained, browser-based German practice site for exam preparation at
levels **B1** and **B2** (Goethe-Zertifikat / telc). Each level offers a written
workbook with hundreds of exercises and an audio module for listening and
speaking, all with instant feedback.

## Features

- **Komplettheft (B1 & B2):** 350 exercises across 7 sections (grammar,
  vocabulary, tenses, prepositions, connectors, reading comprehension, text
  types). Exercise types include multiple choice, fill-in-the-blank, and
  sentence transformation, with paginated sections and live scoring.
- **Hören & Sprechen (B1 & B2):** 50 exercises per module —
  Richtig/Falsch, dictation, text comprehension, pronunciation, free answer,
  and situation tasks. Built on the browser's speech APIs.
- Word-by-word pronunciation accuracy scoring with per-word color feedback.
- Responsive layout, no build step, no backend — just open the HTML files.

## Technology

- **HTML5** and **CSS3** (hand-written, custom palette and layout; no CSS
  framework).
- **Vanilla JavaScript** (no framework, no bundler) for all interactivity,
  scoring, and pagination.
- **Web Speech API** — `SpeechSynthesis` for audio playback and
  `SpeechRecognition` for the speaking exercises (requires Chrome or Edge with
  microphone access).
- **Google Translate TTS** as the primary natural-sounding German voice, with a
  native `SpeechSynthesis` voice as fallback.
- **Bootstrap Icons** (v1.11.3 via CDN) for the UI icons.
- **Google Fonts** — DM Sans.

## Tools

- **[Claude Code](https://claude.com/claude-code)** — used to design and build
  the exercise content, layout, and interaction logic.

## Project structure

```
deutsch/
  index.html                Landing page (level selection)
  b1/
    schriftlich.html        B1 written workbook (350 exercises)
    hoeren-sprechen.html    B1 listening & speaking (Web Speech API)
  b2/
    schriftlich.html        B2 written workbook (350 exercises)
    hoeren-sprechen.html    B2 listening & speaking (Web Speech API)
assets/img/                 Favicons
```

## Usage

Open `deutsch/index.html` in a modern browser and pick a level. For the
**Hören & Sprechen** modules, use **Chrome** or **Edge** and allow microphone
access, since they rely on the Web Speech API.
