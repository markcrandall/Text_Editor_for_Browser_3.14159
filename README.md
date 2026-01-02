# TextEditor
A lightweight, privacy-focused text editor that runs entirely in your browser. No server required, no data leaves your machine.

## Demo / TL;DR
<a href="https://markcrandall.github.io/Text_Editor_for_Browser_3.14159/#H4sIAAAAAAAACm1U0Y7qNhD9lRGVKrZduttKtw_wBAvsRd2FioTeW4kXk0yIhfGk4wlhb9V_r-wsIWFvHvzgOSfjOT4-__Zsb9iL8SwwS7UQw8I64TIRTdb17ntJb9j7IZ59jWE2XcSrNQxg45DhudQpbu3WzhcvM3idLTdbC7DECm6_J0YlCDuj7AFSSsojWvHgF1IpZExHmE4u4FWBFpw6YdpAa8iOqfJ9nRCrPXb5c22wxf9FzgKZ3wvVVLuDx0fqhCDU6va-13QS-l6fgAktxu7Cm1Jlje_fcJW79vWsV2XVHjvN4C-N1UOKBgVvhnReSq9wI-XGpnQrZdgzygkkubL16db4ERf2SpuSxRZyrm16iwx6Zb6wU9yAfoQ1FkYl-B0QVFpy4LruTx3N4nixfI6gn9MJGcLiUETbvVfUIUJSMnuRTsqUeBdEFcUCU82YCPFbLSpmqjQCGZkUGTLi-hZTrQztXTgeWYFIf8PWDO_GFW9ip79hg5urozZvt7iMavtFBRqT5Jgcrr-aXG7f1yAU_RRkHyjLPOkLcQpfWBWt_i_aIlSsiqKLDfvL8rhDbnwT5VSB8QX7XtAWDGYC-1IEGfqM_5Sa0bVarebzoFmc47E9eNBM8QGI4UXvcwHxCA_tR_UFOFBFYd78PShjwGIF2jpRNkEHlEHrZd_Vr3k5hcl47f8xVrUCOzo37WLa7w1CohwOHFqnRZ8QHCpO8tr1kuSQUGkF2jO793l9z6PHoIOMSpt60p-Mp4elv77rt1QnvQ-5gVIh2gurtnww38PYmJbla8NenEYcBm6xvt5632eTIYct_2_tH7O_J6vxegrR59U6ftrEkec-CZufl12uz7p2nAXMqovpRlSDirqoEDD9gulYiAu2D2lDDNPJXUOad0n-oTa1zx9r10fcoJ67qGfytgguvbquY9rVsvad2n1QbmEdsoConU8YVolgyI-ZS1RxY9KuyvdAkmMQO4rH8SaCxXK6eBrHq3XQ-idQmX8J11D3wVfHZR1mrnmJXaPBhETo6D1m1Qlc8F1FnDpQNr2eM4Tt1m7Lx8fHRx8HAx8bQ_j19-I8CvkwyEJ0DGHbmyAf0OAbvJKlbW8ECRniIfB-1__t06d7uCx3I6hyLThwhUpwCAXjwKfCKCRiZqganIeQ6zRFO-r99z8302hsegcAAA" target="_blank">Click Here to try it in your browser.</a>

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



