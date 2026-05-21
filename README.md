# FlashMind — Persistent Study Flashcard App

A clean, fully functional flashcard app where users can create, view, update, and delete study cards that **persist between sessions** using localStorage.

## How to Run

No installation needed. This is a single-file HTML app.

### Option 1 — Open directly in browser
```
1. Download or clone this repository
2. Open index.html in any modern browser (Chrome, Firefox, Edge)
3. That's it — the app runs immediately
```

### Option 2 — Serve locally (optional)
```bash
# Using Python
python -m http.server 8000
# Then open: http://localhost:8000

# Using Node.js
npx serve .
# Then open the URL shown in terminal
```

## Features

- **Create** flashcards with a question, answer, and category
- **Read** all cards in a responsive grid layout
- **Update** any card inline with an edit form
- **Delete** cards with one click
- **Persist** — all data saved to localStorage, survives page refresh and browser close
- **Study Mode** — shuffled card-by-card quiz with reveal mechanic
- **Search & Filter** — find cards by keyword or category
- **5 Categories** — General, Science, History, Tech, Language
- **Toast notifications** — instant feedback on every action

## Tech Stack

- **HTML5 / CSS3** — single file, zero build step
- **React 18** — via CDN (no npm required)
- **localStorage** — for persistence between runs
- **Google Fonts** — Playfair Display + DM Sans

## Project Structure

```
flashcard-app/
├── index.html      # Complete app (HTML + CSS + React/JSX)
├── README.md       # This file
└── ANSWERS.md      # Technical decisions and reflections
```
Built for Dev Weekends Fellowship 2026 Technical Assessment.
