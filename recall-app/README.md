<div align="center">

<img src="favicon.svg" alt="Recall logo" width="84" height="84">

# Recall

**Notes you can actually find.**

A fast, keyboard-friendly notes app for students. Capture notes quickly, find them as you type, and review what you are about to forget.

[![License: MIT](https://img.shields.io/badge/license-MIT-6d4aff.svg)](LICENSE)
![No build step](https://img.shields.io/badge/build-none-2ea44f.svg)
![Vanilla JavaScript](https://img.shields.io/badge/JavaScript-vanilla-f7df1e.svg)
![Data](https://img.shields.io/badge/data-stays%20in%20your%20browser-ff6b8b.svg)

**[Live demo](https://recall-notes-virid.vercel.app/)** · [Report a bug](https://github.com/sikharsethi/recall/issues) · [Request a feature](https://github.com/sikharsethi/recall/issues)

</div>

<!-- Add a screenshot or a short screen recording here, e.g. ![Recall](screenshot.png) -->

## Contents

- [Why Recall](#why-recall)
- [Features](#features)
- [Quick start](#quick-start)
- [Writing notes](#writing-notes)
- [Keyboard shortcuts](#keyboard-shortcuts)
- [How review scheduling works](#how-review-scheduling-works)
- [Import and export](#import-and-export)
- [Your data and privacy](#your-data-and-privacy)
- [Project structure](#project-structure)
- [Deployment](#deployment)
- [Browser support](#browser-support)
- [Limitations](#limitations)
- [Roadmap](#roadmap)
- [Contributing](#contributing)
- [License](#license)

## Why Recall

Study notes end up scattered across chats, screenshots and documents, and finding the right one later takes longer than writing it did. Recall puts them in one place, makes any note reachable in a few keystrokes, and brings old notes back before you forget them.

## Features

**Find things fast**
- Instant search across titles, text, tags and subjects, with highlighted matches. Every word you type must match, and matches in titles and tags rank higher than matches in the body.
- Command palette (`Ctrl/⌘ + K`) with fuzzy matching: jump to any note, filter by subject or tag, or run an action without leaving the keyboard.
- Subjects and tags as filters. Tags are collected automatically from `#hashtags` in your notes.

**Remember what you learn**
- Spaced-repetition review with Again, Good and Easy ratings. Each button shows the next interval.
- Fill-in-the-blank cards: text wrapped in `{{double braces}}` is hidden during review until you reveal it.
- A "revise me" badge on notes that are due, and a daily review streak.

**Capture without friction**
- Four templates: Lecture notes, Cheat sheet, Q&A flashcards and Checklist.
- Import and split: paste a whole chapter and Recall splits it into separate notes at its headings.
- `[[Note links]]` between notes, with a "Linked from" list on the note being linked to.
- Checklists you can tick directly on the note card.

**Take your notes with you**
- Export to Word (`.docx`), Markdown, CSV or a JSON backup. You can export everything or only the current search or filter.
- Dark mode, which follows your system setting and can be switched manually.

## Quick start

There is no build step and nothing to install. Open `index.html` in a browser, or serve the folder:

```bash
npx serve .
```

## Writing notes

Notes are plain text with a few shortcuts:

| You type | You get |
| --- | --- |
| `#tag` | A tag, collected into the tag filters |
| `[[Another note's title]]` | A link to that note. If the note does not exist, clicking the link opens a new note with that title |
| `{{answer}}` | A blank in review mode, shown with a dotted underline in the list |
| `- [ ] task` / `- [x] done` | A checkbox you can tick on the note card |
| `**bold**` | **bold** |
| `` `code` `` | `code` |
| `https://example.com` | A clickable link |

In the note editor, select some text and click **Hide selected text** to wrap it in `{{ }}` for you.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `Ctrl/⌘ + K` | Open or close the command palette |
| `/` | Focus search |
| `N` | New note |
| `R` | Start a review |
| `Esc` (in search) | Clear the search |
| `Ctrl/⌘ + Enter` | Save the note you are writing |
| `Space` or `Enter` (in review) | Reveal the note |
| `1` `2` `3` (in review) | Again, Good, Easy |

Shortcuts for single keys are ignored while you are typing in a field or while a dialog is open.

## How review scheduling works

Every note has a due date. A new note is first due the next day. In review you see up to 20 due notes at a time, oldest first, and rate each one:

| Rating | What happens |
| --- | --- |
| **Again** | The note comes back in about 10 minutes and its interval resets |
| **Good** | Next review in `max(1, round(previous interval × 2.2))` days |
| **Easy** | Next review in `max(3, round(previous interval × 3.5))` days |

This is a simplified version of the idea behind SM-2. It does not track per-note difficulty.

## Import and export

### Import and split

Paste text into **Import** and Recall shows a live preview of how many notes it will create. It starts a new note at:

- lines beginning with `#`, `##` or `###`
- lines like `Chapter 3`, `Unit 2` or `Section 4`
- numbered headings that stand alone on a line, such as `1. What is a stream?`, when the line after them is not another numbered line (so ordinary numbered lists are left alone)
- ALL CAPS lines of at least two words or eight letters

A section longer than about 1,400 characters is split into smaller notes of roughly 900 characters. Text with no headings at all is split the same way. Blank lines between short lines are collapsed. One import creates at most 80 notes, and you can set a subject for all of them.

### Export

| Format | Best for |
| --- | --- |
| **Word (.docx)** | Reading like a document. Subjects become headings, notes become sub-headings, and bold text, code, checklists and bullets are kept. Use *Save as PDF* in Word for a PDF |
| **Markdown (.md)** | Notion, Obsidian, GitHub |
| **CSV (.csv)** | Excel or Google Sheets |
| **JSON backup (.json)** | Full backup including review schedules. Restore it from the New note window under *Backup and restore* |
| **Printable page (.html)** | Opening in a browser and printing |

The Word export loads the [`docx`](https://www.npmjs.com/package/docx) library from a CDN the first time you use it, so that one needs an internet connection.

## Your data and privacy

Notes are stored in your browser's `localStorage`, separately for each website address. Nothing is sent to a server, and there are no accounts or analytics. That also means:

- Clearing your browser's site data deletes your notes. Export a JSON backup now and then.
- Notes do not sync between devices or browsers. Use a JSON backup to move them.

## Project structure

```
recall/
├── index.html     the whole app: markup, styles and JavaScript
├── favicon.svg    logo and browser-tab icon
├── og.png         image shown when the link is shared
├── README.md
└── LICENSE
```

The app is one HTML file by design, so it can be opened directly and hosted anywhere that serves static files.

## Deployment

Any static host works. With Vercel:

1. Push this repository to GitHub.
2. Import it at [vercel.com/new](https://vercel.com/new), keep the framework as **Other** and leave the build command empty.
3. Deploy. Every later push to `main` redeploys automatically.

After the first deploy, replace `YOUR-SITE.vercel.app` in the `og:image` tag of `index.html` with your real address, so link previews on X and other sites show the card image.

## Browser support

Recent versions of Chrome, Edge, Safari and Firefox. The app uses the `<dialog>` element, CSS `color-mix()` and CSS columns. Older browsers may display it incorrectly.

## Limitations

- No sync, accounts or sharing. Data lives in one browser.
- Import splits text with simple rules. It works best on text with clear headings, and unusual formatting may need a manual edit afterwards.
- Review scheduling is simplified, as described above.
- Search matches words inside notes. It does not understand meaning or fix spelling mistakes (only the command palette is fuzzy).

## Roadmap

Ideas, not promises:

- [ ] Study statistics: review heatmap and weakest subjects
- [ ] Optional sync across devices
- [ ] Direct PDF export
- [ ] Image attachments

## Contributing

Issues and pull requests are welcome. Because the project is a single file with no build step, you can make a change, open `index.html` in a browser and see it straight away. For larger changes, please open an issue first to discuss the idea.

## License

Released under the [MIT License](LICENSE).

---

<div align="center">Built by <strong>Sikhar Sethi</strong> · <a href="https://github.com/YOUR-USERNAME">GitHub</a></div>