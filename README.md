<div align="center">

# 🧠 FlashMind

### Persistent Study Flashcard App

*Create, study, and master flashcards — all saved right in your browser.*

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![React](https://img.shields.io/badge/React_18-61DAFB?style=for-the-badge&logo=react&logoColor=black)
![LocalStorage](https://img.shields.io/badge/Persistence-localStorage-C9A84C?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Complete-2a9d8f?style=for-the-badge)

[⚡ Quick Start](#-quick-start) · [✨ Features](#-features) · [🛠️ Tech Stack](#️-tech-stack) · [📁 Project Structure](#-project-structure)

</div>

---

## 📌 About

**FlashMind** is a clean, fully functional flashcard app for studying. Users can create, view, update, and delete study cards, and everything **persists between sessions** using `localStorage` — no backend, no database, no build step.

It was built as a single self-contained HTML file for the **Dev Weekends Fellowship 2026 Technical Assessment**, with the constraint that it had to run with zero installation.

---

## ✨ Features

- **Create** flashcards with a question, answer, and category
- **Read** all cards in a responsive grid layout
- **Update** any card inline with an edit form
- **Delete** cards with one click
- **Persist** — all data saved to `localStorage`, survives page refresh and browser close
- **Study Mode** — shuffled card-by-card quiz with a reveal mechanic
- **Search & Filter** — find cards by keyword or category
- **5 Categories** — General, Science, History, Tech, Language
- **Toast notifications** — instant feedback on every action

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Markup | HTML5 |
| Styling | CSS3 (custom, single-file, dark navy/gold theme) |
| UI Framework | React 18 (via CDN — no npm required) |
| Persistence | Browser `localStorage` |
| Fonts | Google Fonts — Playfair Display + DM Sans |
| Build step | None — open and run |

---

## 📁 Project Structure

```
flashmind/
├── index.html      # Complete app — HTML + CSS + React/JSX in one file
├── README.md       # This file
└── ANSWERS.md       # Technical decisions, edge cases, and reflections
```

---

## ⚡ Quick Start

No installation needed — this is a single-file HTML app.

### Option 1 — Open directly in browser
```bash
git clone https://github.com/mehmoona-chand/flashmind.git
cd flashmind
# Open index.html in any modern browser (Chrome, Firefox, Edge)
```

### Option 2 — Serve locally (optional)
```bash
# Using Python
python -m http.server 8000
# Then open: http://localhost:8000

# Using Node.js
npx serve .
# Then open the URL shown in the terminal
```

---

## 🧩 Notable Engineering Decisions

These are pulled from `ANSWERS.md` in the repo:

- **Single JSON array, one key** — all cards are stored under one `localStorage` key (`flashmind_cards_v1`) rather than one key per card, so loading/saving is a single read/write instead of N separate ones.
- **Corrupted-data handling** — the `useLocalStorage` hook wraps `JSON.parse` in a `try/catch`. If the stored data is malformed, the app falls back to an empty array instead of crashing to a blank white screen.
- **Simplicity over backend** — a backend (Node + SQLite) was considered and rejected for this scope; it would add a server, installation steps, and failure points for what is fundamentally a single-user app.

---

## 🗺️ Known Limitations

- Search and filter are client-side only; there's no sort-order control (cards always show newest-first).
- No spaced-repetition logic yet — a planned next step is letting users mark a card "Easy / Medium / Hard" after studying, and prioritizing harder cards on future review (similar to Anki).



---

## 👩‍💻 Author

**Mehmoona Chand (Sylvia)**
BS Information Technology
Dev Weekends Fellow 2026 | Aspiring DevOps & Cloud Engineer

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/mehmoonachand)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat&logo=github)](https://github.com/mehmoona-chand)

---

<div align="center">

⭐ **Star this repo if you find it useful!**

Built for the Dev Weekends Fellowship 2026 Technical Assessment 💛

</div>
