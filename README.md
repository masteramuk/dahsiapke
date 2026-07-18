# dahsiapke

> Copyright © 2026 haszeli.ahmad. All rights reserved.

A completely offline personal Kanban dashboard. Open `index.html` directly in a modern laptop browser; no server, build step, account, or network connection is required.

Documentation:

- [HELPME.md](HELPME.md) — download, setup, saving, backup, and troubleshooting quick start
- [USERMANUAL.md](USERMANUAL.md) — complete guide to every page, button, field, and interaction

Both guides are bundled into `help-content.js` and displayed through the application's **Help** page. The responsive support QR is generated as inline SVG by `index.html`, so no QR image file is required in a public distribution.

## Data files

The application intentionally uses seven separate task JSON array files:

- `bakul_kerja.json` — the underlying regular work dataset, presented through the **Work Bucket** all-active-work view
- `fokus_kerja.json` — the underlying focus dataset, presented as **Critical & Important** together with other high-priority or at-risk work
- `tengah_buat.json` — **In Progress** and Review workflow data
- `dah_siap.json` — **Done** tasks, which are read-only in the UI
- `batal_kerja.json` — **Work Cancel**, retained as closed history
- `tunda_kerja.json` — **Task On Hold**
- `archive_kerja.json` — completed work moved out of the active Done dataset

An additional append-only audit dataset is used for change tracking:

- `change_history.json` — task creation, edits, status/bucket movements, completion, time changes, hold/cancel actions, critical marking, archive, and restore events

Every task contains the required fields: `id`, `title`, `description`, `category`, `priority`, `important`, `status`, `time_spent_mins`, and `created_at`. `completed_at`, `expected_start_date`, `expected_completion_date`, `progress_percent`, `parent_task_id`, `depends_on`, and `reference_people` enable archiving, scheduling, task families, searchable multi-task dependency paths, and key-contact context. Older Done files without `completed_at` remain compatible; completion is inferred from expected completion date and then creation date.

The automatic archive policy runs after files are loaded. It always keeps the three most recently completed tasks in active Done and archives any other Done task whose `completed_at` is older than three calendar months. Every active Done card also has an **Archive** button; manual archive and restore actions remain available on the Archive page.

## Use

1. Double-click `index.html`.
2. The app first tries to read all eight adjacent JSON files. If the browser blocks this, click **Connect Data Folder**, select the project folder once, and approve read/write access.
3. Use the dedicated **Dashboard**, **Work Board**, **Critical Path**, **Archive**, **Change History**, and **Help** pages. Edit active cards, drag work, filter the board, search large parent/dependency lists, and log time in 15-minute increments. Done cards are read-only but can be archived directly.
4. Changes are safety-cached in IndexedDB while you work. Click **Save Changes** to write all eight JSON files together through the connected folder. If direct writing is unavailable, the app downloads one combined `dahsiapke_backup.json` instead.

History begins when the history-enabled application records a new mutation. Changes made before this feature existed cannot be reconstructed. History entries are append-only in normal application use and record the actor as `Local user` because the application has no accounts.

The JSON files are the startup source of truth; browser memory is not restored over them. Direct JSON updates require one explicit folder selection and write permission because the application cannot access unrelated local files.

## Security and performance

- Imported task and history JSON is size-limited and schema-validated.
- Duplicate IDs, invalid statuses/priorities, unsafe numeric values, and malformed datasets are rejected.
- User-controlled text is rendered with `textContent`, never injected as HTML, preventing stored XSS through imported task data.
- No secrets, remote dependencies, telemetry, cookies, or external network calls are used. IndexedDB is a guarded safety cache; the eight JSON files remain the startup source of truth.
- Rendering is designed for personal datasets and accepts at most 5,000 tasks per task file (5 MB each) and 50,000 audit events (20 MB).

## Copyright and licence

Copyright © 2026 haszeli.ahmad. All rights reserved. Personal, non-commercial use is permitted under [LICENSE.md](LICENSE.md). Commercial use, resale, sublicensing for payment, or monetised distribution requires prior written consent and a separate written profit-sharing agreement with haszeli.ahmad.
