# Recall

**Notes you can actually find.** Recall is a fast, keyboard-friendly notes app for students: dump notes quickly, find them instantly, and review what you are about to forget.

> **Live demo:** _add your Vercel link here_
>
> _Tip: add a screenshot or a short screen recording here, for example `![Recall](screenshot.png)`._

## Features

- **Instant search** across titles, text, tags and subjects, with highlighted matches and typo tolerance.
- **Command palette** (`Ctrl/⌘ + K`): jump to any note or run an action from the keyboard.
- **Spaced-repetition review:** rate notes Again, Good or Easy and Recall schedules the next review. Notes due today are flagged.
- **Fill-in-the-blank cards:** wrap text in `{{double braces}}` and Review hides it until you reveal it.
- **`[[Note links]]`** between notes, with a "Linked from" list on the linked note.
- **Checklists** (`- [ ] task`) you can tick directly on the note card.
- **Import and split:** paste a whole chapter and it is split into separate notes at its headings.
- **Templates:** Lecture notes, Cheat sheet, Q&A flashcards and Checklist.
- **Export** to Word (`.docx`), Markdown, CSV or a JSON backup. The current search or filter can be exported on its own.
- Subject colours, tags, pinning, undo on delete, dark mode.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Ctrl/⌘ + K` | Command palette |
| `/` | Focus search |
| `N` | New note |
| `R` | Start a review |
| `Ctrl/⌘ + Enter` | Save the note you are writing |
| `Space` / `1` `2` `3` | In review: reveal, then Again / Good / Easy |

## Run it locally

There is no build step. Open `index.html` in a browser, or serve the folder:

```bash
npx serve .
```

## Deploy

Push the repository to GitHub, then import it at [vercel.com/new](https://vercel.com/new). Leave the framework as **Other** and the build command empty. After the first deploy, replace `YOUR-SITE.vercel.app` in the `og:image` tag of `index.html` with your real address so link previews on X and other sites show the card image.

## Tech

Plain HTML, CSS and JavaScript in a single file. No framework and no backend. The Word export loads the [`docx`](https://www.npmjs.com/package/docx) library from a CDN only when you use it.

## Your data

Notes are stored in your browser's `localStorage`. Nothing is sent to a server. Clearing site data removes your notes, so use **Export → JSON backup** now and then. A JSON backup can be restored from the New note window (Backup and restore).
