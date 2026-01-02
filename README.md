# TextEditor
A lightweight, privacy-focused text editor that runs entirely in your browser. No server required, no data leaves your machine.

## Demo / TL;DR
<a href="https://markcrandall.github.io/Text_Editor_for_Browser_3.14159/#H4sIAAAAAAAACm1UwY7iRhD9lZKjRDPZJcNecoATDLCLMgMRNrsbiUthl3Fr2l1WdxkzG-Xfo24PxjDrgw9d77mqn9-rfyMTjaKETgLzTAlbWBontk5FsXHRxyiNRtEvyfx7AvPZMllvYABbRxY-1yqjndmZxfJpDs_z1XZnAFbUwO3zaAmFYK_RvEDGaV2SEQ9-Yswgt1zCbHoGrysy4PBIWQdtIXvLje_rhC0e6Jq_UJp6_D_kJJD7s1DNlHvx-BiPBMK9bm9nXSfhn_UJmNBi4s68GTdG-_4dF92lr2c9o8EDXTWDr4qah4w0Cd1c0nkpvcKdlFuT8a2U4UyjE0gLNO10G3qPC2e1ydhQD7lQJrtFBr1yX9ij7UC_wYYqjSn9BASNkgJsW_dTx_MkWa4-x3BX8JEshJcjEWUOXlFHBGltrRfpiLqm-yCqoBWYKUupsH1tRaUcay2Qs87IQs62_YuZQs0HF8ZjIxCrH9S7w5txxZvYqR_U4RZYKv16i8u5tV9ckdZpQenL5VPT89_3NQhFfws2D5znnvSNbQbfLFa9_k_KEDQWq-oamxRU9ucMV0T7AmzhSR0KAfEID72LW70cYFXpVy8bag2GGlDGCZqUHHAOvSDet-FbzWA62fhvTLAdeM-nrl3Ch4MmSNHRwJFxStSRwBHatGhNKmkBKddGLpEouHFg6nLvf2YOpceQg5xrk3nS35aODyuv9uVZ4VEdQsxJGiJzZrUODV55mGjdc2jrr7Mx2IYL91jfb63qV4lmRz277sxf83-m68lmBvGX9SZ53Cax5z6K1R9W11y_mvrbJ2DW15jrjdKh4mtU2Ad3leWyEhdcGpYDW5hN7zvS4prkc9XVvryvXTIXrIP7d5dfGkdWQHDvM20xFQqJnbsUqxufXQv1EVgKCnrFySTZxrBczZaPk2S9CXL9DpgL2d4a9aumXVDt-nCd96-9AlMW4dLbxOARXLBOwzZzgCa7zOnXWz0cDoc-fAMf0hF8-rM6jUMaB3kI6gh20ZTsC2l6hWc2vIvG0BRKaOAqTGkElaVx2C-55mbgIzcCw7ZEPYZGZVKMoMTTIGUjZGQMpTKDt_NPw-Gv4-i__wGJQDGx8AYAAA" target="_blank">Click Here to try it in your browser.</a>

## Overview

TextEditor is a single HTML file (~1250 lines) that provides a complete text editing experience. It combines the simplicity of a plain text editor with modern features like URL-based document sharing, local database storage, and a clean dark/light theme interface.

### Key Features

- **Zero Installation** - Open `index.html` in any modern browser
- **Complete Privacy** - All data stays in your browser (localStorage and IndexedDB)
- **URL Sharing** - Documents compress into shareable URLs using gzip + base64 encoding
- **Dual Storage** - Save to browser database (IndexedDB) or export to disk (.txt files)
- **Auto-Save** - Content automatically saves to URL hash after 500ms of inactivity
- **Find & Replace** - Full-featured search with case sensitivity and match counting
- **Customizable** - Font size, font family, spellcheck, word wrap, line numbers, and theme
- **Offline Ready** - Works without internet connection once loaded

### Technical Highlights

- Uses `contenteditable="plaintext-only"` for clean text editing
- Leverages modern browser APIs: CompressionStream, File System Access API, IndexedDB
- Graceful fallbacks for older browsers (file input for Firefox/Safari)
- Single undo/redo stack for replace-all operations via execCommand
- Local Fonts API integration for font selection (Chrome 103+)

## Browser Support

- **Chrome/Edge 80+** - Full functionality including File System Access API
- **Firefox/Safari** - Core features with fallback file handling

---

# User Guide

## File Menu

| Option | Description |
|--------|-------------|
| New | Create blank document |
| Load from DB | Open saved document from browser storage |
| Load from File | Open .txt file from disk |
| Save to DB | Save document to browser storage |
| Save File (overwrite) | Overwrite previously opened file (appears after opening a file) |
| Save File As | Download document as .txt file |
| Manage DB | View/delete saved documents |

## Edit Menu

| Option | Description |
|--------|-------------|
| Undo | Undo last change |
| Redo | Redo undone change |
| Find | Open find bar |
| Find & Replace | Open find bar with replace options |

## Settings

Hover over any setting to see its current value. Settings persist across sessions.

| Setting | Description |
|---------|-------------|
| Start Directory | Default folder for file dialogs (documents, downloads, desktop) |
| Font Size | Editor text size (10-48 pixels) |
| Font Family | Editor font (uses Local Fonts API on Chrome 103+) |
| Spellcheck | Browser spell checking on/off |
| Word Wrap | Line wrapping on/off |
| Line Numbers | Show line numbers in left gutter (requires Word Wrap OFF) |
| Theme | Dark or Light theme |

## Find Bar

| Element | Description |
|---------|-------------|
| Aa checkbox | Toggle case-sensitive search |
| Match count | Shows number of matches found |
| Prev/Next | Navigate between matches |
| Replace/All | Replace current match or all matches |
| X | Close find bar |

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| Ctrl+N | New document |
| Ctrl+O | Load from File |
| Ctrl+S | Save (prompts for File or DB) |
| Ctrl+F | Find |
| Ctrl+H | Find & Replace |
| Ctrl+G | Go to Line (requires Line Numbers ON) |
| Tab | Insert tab character |
| Escape | Close find bar |

## Status Indicators

| Indicator | Meaning |
|-----------|---------|
| * after "File" | Unsaved changes |
| Word count | Bottom of navigation shows word and character count |

---

## How It Works

### URL-Based Storage

When you type, your content is automatically compressed using gzip and encoded as a URL-safe base64 string in the URL hash. This means:

1. Your document is stored in the URL itself
2. Browser history tracks document versions
3. Sharing the URL shares the document
4. Bookmarking saves the document state

### Browser Database (IndexedDB)

For longer-term storage, save documents to the browser's IndexedDB:

- Documents persist across browser sessions
- Manage multiple named documents
- Quick access via "Load from DB"

### File System

Export documents to disk as `.txt` files, or open existing text files for editing. On Chrome/Edge, the File System Access API enables direct file overwriting.


