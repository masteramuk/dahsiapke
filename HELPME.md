# dahsiapke — Quick Start and Help

> Copyright © 2026 haszeli.ahmad. All rights reserved. Commercial use requires prior written consent and an agreed profit-sharing arrangement.

`dahsiapke` is a completely offline personal Kanban and productivity dashboard. It runs directly from a local folder in a modern browser. It does not require installation, a server, an account, or an internet connection.

## Important: how saving works

The eight JSON files beside `index.html` are the startup source of truth. The application first tries to read them automatically. If browser security blocks direct sibling-file access, click **Connect Data Folder** once and select the `dahsiapke` folder. A previously approved folder is loaded automatically while its permission remains valid.

IndexedDB is used only as a safety cache while you work; reopening the application does not replace the JSON source with stale browser memory.

The storage-status line reports whether the automatic local save succeeded and whether JSON synchronization remains pending.

Click **Save Changes** to synchronize the working state with the eight JSON files:

- In a supported Chromium browser such as Chrome or Edge, approve the data folder once. The application updates all eight files together without asking about each file.
- If direct folder writing is unavailable, the application downloads one `dahsiapke_backup.json` containing all datasets and Change History. That combined backup can be loaded through the compatibility file picker.

```text
Connect Data Folder → Work (safety-cached locally) → Save Changes → Synchronize eight JSON files
```

The JSON synchronization step still requires a button click and explicit permission. Browser security does not allow an offline page to write arbitrary laptop files silently.

## Download or copy the application

If the application is supplied as a ZIP file:

1. Download the ZIP file.
2. Extract it into a permanent folder, for example `Documents/dahsiapke`.
3. Keep `index.html` and all JSON files together in that folder.

If the application is stored in a source repository:

1. Download the repository as a ZIP or clone it.
2. Extract or copy the `dahsiapke` folder to a permanent local location.
3. Do not run the application from inside a compressed ZIP archive.

The folder should contain:

```text
dahsiapke/
├── index.html
├── bakul_kerja.json
├── fokus_kerja.json
├── tengah_buat.json
├── dah_siap.json
├── batal_kerja.json
├── tunda_kerja.json
├── archive_kerja.json
├── change_history.json
├── help-content.js
├── HELPME.md
├── USERMANUAL.md
├── LICENSE.md
└── README.md
```

`help-content.js` is the offline copy used by the in-app Help page. The support QR is generated as an SVG by the JavaScript embedded in `index.html`, so no separate QR image is required.

## Start using dahsiapke

1. Open the `dahsiapke` folder.
2. Double-click `index.html`.
3. A modern browser should open the application.
4. Allow the automatic JSON load to complete. If it is blocked, click **Connect Data Folder**.
5. Select the `dahsiapke` folder itself and approve read/write access once.
6. Begin working from the Dashboard or Work Board.

The expected filenames are:

- `bakul_kerja.json`
- `fokus_kerja.json`
- `tengah_buat.json`
- `dah_siap.json`
- `batal_kerja.json`
- `tunda_kerja.json`
- `archive_kerja.json`
- `change_history.json`

Filenames must remain unchanged so the application can identify each dataset.

## Start with empty datasets

The supplied JSON files may contain example records. To start completely empty, each dataset must contain a valid empty JSON array:

```json
[]
```

Do not leave a JSON file blank. A blank file is not valid JSON.

## Save and close safely

1. Confirm that the storage-status line says the browser safety copy was saved.
2. Click **Save Changes**.
3. If prompted, approve the connected data folder once.
4. Wait for the success message confirming that all eight files were updated together.
5. You may then close the application. The JSON files will be loaded again at the next session.

If the browser cannot update the files directly, keep the single downloaded `dahsiapke_backup.json` as the portable backup.

## Recommended backup practice

Before replacing the old files, periodically copy them into a dated backup folder:

```text
backups/
└── 2026-07-15/
    ├── bakul_kerja.json
    ├── fokus_kerja.json
    ├── tengah_buat.json
    ├── dah_siap.json
    ├── batal_kerja.json
    ├── tunda_kerja.json
    ├── archive_kerja.json
    └── change_history.json
```

Do not merge JSON files manually unless you understand the task IDs and schema. Duplicate task IDs are rejected during import.

## Common problems

### My work disappeared after reopening

Open the same `index.html` file and confirm that all eight JSON files remain beside it. If the browser cannot load them automatically, click **Connect Data Folder** and choose their folder. The app intentionally does not restore task data from browser memory at startup.

### The browser downloaded only one file

This is expected only on the compatibility path: the file should be `dahsiapke_backup.json`, containing all eight datasets. In Chrome or Edge, use **Connect Data Folder** so **Save Changes** can update all eight source files directly.

### A file is rejected as unknown

Check that its filename exactly matches one of the eight expected names. Remove suffixes such as `(1)` that the browser may have added.

### A file is rejected as invalid JSON

Open the file in a text editor and confirm that it contains a JSON array beginning with `[` and ending with `]`. Do not use comments or trailing commas inside JSON.

### A duplicate task ID is reported

The same task exists in more than one task dataset. Each task ID must appear in only one of the seven task files.

### Drag and drop is difficult on a phone

Native browser drag and drop is most reliable with a mouse or trackpad. On a phone, use the card's **Edit** button and change its Status. The board columns can be swiped horizontally.

### An old Done task returns to Archive after restoration

The automatic archive rule runs after datasets are loaded. It keeps the three most recently completed tasks in active Done and archives other Done tasks older than three calendar months. An older restored task may become eligible again during the next load.

### Archive one Done task now

Open **Work Board**, choose the **Done** view, and click **Archive** on the completed task card. The task moves to `archive_kerja.json`, remains available for **Restore** on the Archive page, and is recorded in Change History. Click **Save Changes** to synchronize the JSON files.

### I accidentally deleted a task

Deletion is confirmed and then saved to the browser-local database. After **Save Changes** synchronizes the JSON files, recovery requires an older JSON backup or combined backup. Change History records the deletion but does not recreate the task automatically.

## Offline and privacy guarantees

- No external network request is made; the startup reader only attempts the JSON files beside `index.html`.
- No login, cookie, telemetry, or analytics is used.
- No data is uploaded anywhere.
- All task text is rendered safely instead of being injected as HTML.
- Imported files are validated and size-limited.

For a complete description of every page, button, field, and interaction, read [USERMANUAL.md](USERMANUAL.md).

Both guides are also available inside the application: open **Help** in the main navigation and choose Quick Help or Full User Manual.
