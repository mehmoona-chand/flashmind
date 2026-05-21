# ANSWERS.md — FlashMind Technical Assessment

## 1. How to Run

No installation or build step required.

```
1. Clone or download this repository
2. Open index.html in any modern browser (Chrome, Firefox, Edge)
3. The app runs immediately — no npm install, no server needed
```

To serve locally (optional):
```bash
python -m http.server 8000
# Visit http://localhost:8000
```

All data persists automatically in the browser's localStorage.

---

## 2. Stack Choice

**I chose: React 18 (CDN) + localStorage + single HTML file**

### Why this stack?
- **React via CDN** — lets me use component-based architecture and hooks (useState, useEffect) without requiring Node.js or a build tool. Anyone can open the file and it works instantly.
- **localStorage** — the right tool for this scale. It's synchronous, zero-latency, requires no backend, and perfectly fits a single-user flashcard app. Data survives page refreshes, tab closes, and browser restarts.
- **Single HTML file** — the simplest possible delivery. No dependencies to install, no version conflicts, no build pipeline to explain.

### What would have been a worse choice and why?
- **IndexedDB directly** — unnecessarily complex API for simple key-value storage. Async API adds boilerplate without real benefit at this scale.
- **A backend (Node + SQLite)** — would require installation steps, a running server, and adds failure points. Overkill for a personal flashcard app.
- **Vue or Svelte** — also good frameworks, but React's ecosystem familiarity and CDN availability made it the faster, more justifiable choice here.

---

## 3. One Real Edge Case

**Edge case: corrupted or invalid JSON in localStorage**

**File:** `index.html`  
**Line:** Inside the `useLocalStorage` hook, approximately line 110–120:

```javascript
const [value, setValue] = useState(() => {
  try {
    const stored = localStorage.getItem(key);
    // EDGE CASE: corrupted JSON in localStorage — fall back to initial
    return stored ? JSON.parse(stored) : initial;
  } catch(e) {
    console.warn('FlashMind: localStorage parse error, resetting.', e);
    return initial;
  }
});
```

**What this handles:**  
If the browser's localStorage contains malformed data (e.g. the user manually edited it, a write was interrupted mid-save, or another script corrupted the value), `JSON.parse()` throws a SyntaxError. Without this try/catch, the entire app would crash on load with a blank white screen and the user would lose access to all their cards.

**Without this handling:**  
`JSON.parse("{broken")` throws `SyntaxError: Unexpected token b` — the app crashes immediately on startup, showing nothing. The user has no way to recover without manually clearing localStorage from DevTools.

**With this handling:**  
The app catches the error, logs a warning, and gracefully falls back to an empty array. The user sees a working app with no cards rather than a broken white screen.

---

## 4. AI Usage

I used **ChatGPT** during this project in the following ways:

| Where | What I asked | What it gave | What I changed |
|---|---|---|---|
| CSS animation | "How to animate a card sliding in on mount in CSS" | Suggested `@keyframes` with `translateY` | I kept the keyframe but adjusted timing from 0.5s to 0.3s — 0.5s felt sluggish for a UI element |
| localStorage hook | "Best pattern for syncing React state with localStorage" | Suggested a `useLocalStorage` custom hook with `useEffect` | I added the `try/catch` for JSON parse errors — the AI version assumed the stored data would always be valid, which is not realistic |
| Study mode shuffle | "How to shuffle an array in JavaScript" | Gave the Fisher-Yates algorithm | I used the simpler `.sort(() => Math.random() - 0.5)` instead — less theoretically perfect but readable and sufficient for flashcard counts under 1000 |

**One output I changed and why:**  
The AI suggested storing each card as a separate localStorage key (e.g. `card_1`, `card_2`). I changed this to store all cards as a single JSON array under one key (`flashmind_cards_v1`). The AI's approach would work but requires listing all keys on load and doing N separate reads. A single key means one read, one write — simpler, faster, and easier to debug.

---

## 5. Honest Gap

**What isn't good enough:** The search and filter are client-side only and there is no sort order control. Cards always appear newest-first and there is no way to sort by category, alphabetically, or by "last studied." For a serious study app, you would want to sort by difficulty or last review date (spaced repetition).

**What I would do with another day:**  
Implement a basic spaced repetition system — after studying a card, the user marks it as "Easy," "Medium," or "Hard." The app would then prioritize showing hard cards more frequently and push easy cards further into the future. This is the core algorithm behind apps like Anki, and it would transform FlashMind from a simple CRUD demo into a genuinely useful learning tool. I would store a `nextReview` timestamp and `difficulty` score on each card in localStorage.
