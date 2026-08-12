# Perpustakaan GSJA Betlehem Bogor — Library App Prototype

A mobile app prototype for the **GSJA Betlehem Bogor** church library. Members can
browse the collection, borrow and return books, join a waitlist for titles that are
out, track due dates, and suggest new books — all from an iPhone-sized interface.

The UI is in **Indonesian** (Bahasa Indonesia). This is a front-end **prototype**:
all data lives in-memory in the browser, there is no backend, and nothing is persisted.

> Status: Prototype v2 · No build step required for the standalone version.

## Features

- **Beranda (Home)** — greeting, a status card showing books currently on loan
  (limit 3 per member), overdue alerts, "new arrivals" and "frequently borrowed"
  discovery rails, and quick search.
- **Katalog (Catalog)** — full collection with search, category chips
  (Renungan, Teologi, Doa, Biografi), sorting (title / author / popularity / rating),
  and an "available only" toggle.
- **Detail buku (Book detail)** — cover, rating and reviews, availability, description,
  and metadata (publisher, year, pages, ISBN, language, shelf location).
- **Peminjaman (Borrowing)** — confirm-to-borrow sheet with a generated 6-digit pickup
  code and barcode; enforces the 3-book borrowing limit.
- **Pengembalian (Return)** — return sheet with a scannable code for the front desk.
- **Antrean (Reservations)** — join a waitlist when all copies are out.
- **Perpanjang (Renew)** — extend a loan once.
- **Pinjaman saya (My loans)** — active loans, reservation queue, and return history.
- **Profil (Profile)** — member stats, notification toggles, help/contact, library
  hours, and a "suggest a new book" form.
- Splash screen, toasts, bottom tab navigation, and reduced-motion support.

## Project structure

```
project/
├── uploads/
│   ├── index.html                     # Standalone prototype (open this in a browser)
│   └── gsja-library/
│       ├── index.html                 # Identical standalone prototype
│       ├── logo-GSJA-png.png          # Church logo (PNG)
│       └── logo-GSJA-jpg.jpg          # Church logo (JPG)
├── Perpustakaan GSJA.dc.html          # DesignComposer version (React runtime)
├── support.js                         # Generated dc-runtime bundle (used by the .dc.html)
├── ios-frame.jsx                      # iOS 26 device-frame component for the .dc.html
├── .thumbnail                         # Preview thumbnail metadata
└── README.md
```

### Two versions of the app

1. **Standalone HTML** (`uploads/index.html`) — a single self-contained file with all
   HTML, CSS, and vanilla JavaScript inline. No dependencies, no build, no server.
   This is the easiest way to see the app.

2. **DesignComposer** (`Perpustakaan GSJA.dc.html`) — the same app authored in a
   component/template format that uses custom tags (`x-dc`, `sc-if`, `sc-for`,
   `x-import`). It is rendered by React through the generated `support.js` runtime and
   wraps the screen in the `ios-frame.jsx` device frame. `support.js` is generated code —
   do not edit it by hand.

## Running it

### Standalone version (recommended)

Just open the file in any modern browser:

```bash
# from the project directory
start "" "uploads/index.html"     # Windows
```

Or serve the folder over HTTP (needed if you want the logo images and relative paths to
resolve cleanly):

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000/uploads/`.

### DesignComposer version

`Perpustakaan GSJA.dc.html` loads `support.js`, which expects React/ReactDOM to be
available and processes the `x-dc` template at runtime. Serve the project root over HTTP
and open the file through the server (opening it directly from the filesystem may fail
due to script/module loading):

```bash
python -m http.server 8000
# then open http://localhost:8000/Perpustakaan%20GSJA.dc.html
```

## Tech notes

- **Standalone app:** plain HTML + CSS + vanilla JavaScript. State (loans, reservations,
  member info) is held in JS variables and re-rendered on change — nothing is saved
  between reloads.
- **Fonts:** Inter, loaded from Google Fonts.
- **Design:** iPhone-style mobile frame, light theme, with a full breakpoint that goes
  edge-to-edge on narrow screens.
- **Data:** the book catalog is a hard-coded array in the script; a real deployment would
  replace it with an API.

## License

No license specified. Add one if you intend to share or reuse this code.
