# Cull

A quiet, single-page image triage tool. Step through a folder of images, keep what works and cull the rest, then walk away with a delete list, or remove the rejects on the spot. **100% client-side**: nothing is uploaded, everything stays in your browser.

## What it does

1. **Choose a folder** of images.
2. **Mark** each frame: keep (○) or cull (✕) — by mouse, or with `←` / `→` arrow keys (`Z` undo, `B` cycles the backdrop).
3. At the end, handle the culled ones two ways:
   - **Copy a delete prompt** — a ready-to-paste prompt telling Claude Code exactly which files to delete. Works in every browser.
   - **Delete them directly** — in Chrome/Edge the tool uses the File System Access API to remove the culled files from the folder itself (one click, with a confirm). Needs a secure context (HTTPS).

Decisions are saved in the browser by filename, so you can close the tab and resume.

## Privacy

No server, no upload, no analytics. Images are read locally via the folder picker and rendered from in-memory object URLs. The direct-delete feature only touches files in the folder you explicitly granted access to.

## Tech

A single self-contained `index.html`: vanilla JS, no build step, no dependencies (Google Fonts is the only external request). Deploy by serving the file statically.

## Run locally

Open `index.html` in any browser. The **direct-delete** path needs a secure context (HTTPS or `localhost`), so on a raw `file://` open you get the copy-prompt path only.
