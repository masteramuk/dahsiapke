# dahsiapke — User Manual

> Copyright © 2026 haszeli.ahmad. All rights reserved. Commercial use requires prior written consent and an agreed profit-sharing arrangement.

## 1. Start here after downloading

Follow these steps before creating or changing any work:

1. Download the complete `dahsiapke` folder or ZIP package.
2. If it is a ZIP package, extract it into a permanent folder. Do not run the application from inside the ZIP file.
3. Open the extracted `dahsiapke` folder.
4. Double-click **`index.html`**.
5. The application opens in your default browser. Chrome or Edge is recommended when you want **Save Changes** to update the original JSON files directly.

No installation, server, account, or internet connection is required.

## 2. Load all JSON files before using the application

Do not start creating or editing tasks until the complete data set has loaded.

1. The application first tries to read the eight JSON files beside `index.html` automatically.
2. If the browser blocks that direct access, click **Connect Data Folder** in the header.
3. Select the extracted `dahsiapke` folder itself, then approve read and write access once. Do not select the files individually.
4. Wait for the success message confirming that all eight JSON files were loaded.
5. Review the Dashboard totals before continuing. If the totals are unexpected, stop and load the correct files.

The required files are:

| Required JSON file | Data contained |
|---|---|
| `bakul_kerja.json` | Regular To Do work |
| `fokus_kerja.json` | Focused Critical & Important To Do work |
| `tengah_buat.json` | In Progress and Review work |
| `dah_siap.json` | Active Done work |
| `batal_kerja.json` | Cancelled and closed work |
| `tunda_kerja.json` | Work placed on hold |
| `archive_kerja.json` | Archived completed work |
| `change_history.json` | Append-only change events |

All filenames must remain unchanged. The application rejects an incomplete data folder so task counts, dependencies, archive records, and Change History cannot silently load as a partial set.

You may alternatively load one previously generated `dahsiapke_backup.json`. That combined backup contains all eight datasets.

## 3. Understand how your work is saved

The eight JSON files are the startup source of truth. After they load, `dahsiapke` also stores the working state in IndexedDB as a safety cache while you work. The safety cache is not used to replace the JSON files when the application starts.

Check the storage-status line near the top of the application:

- **Saved automatically in IndexedDB:** the temporary browser safety copy is safe.
- **JSON sync pending:** the browser-local copy contains changes that have not yet been written to the eight JSON files.
- **Automatic local saving failed:** stop working and use **Save Changes** immediately.

The **Save Changes** button writes all eight JSON files in one operation. In Chrome or Edge, the application asks for one data-folder permission, not eight file permissions. In browsers without direct folder-writing support, the application downloads one `dahsiapke_backup.json` instead.

The following sections explain every page and button. The final section provides the required synchronization checklist to complete before closing the application.

## 4. Header controls

### Dashboard

Opens the high-level productivity summary.

### Work Board

Opens the Kanban board and work views.

### Critical Path

Opens task dependency and critical-path analysis.

### Archive

Opens completed-work search, grouping, sorting, archiving, and restoration.

### Change History

Opens the append-only audit timeline.

### Help

Opens the in-app documentation viewer. Choose Quick Help or Full User Manual without opening a terminal, editor, external application, or internet page.

The Help page also shows a code-generated support QR beside either guide on wide screens. The support card remains visible while the guide scrolls and moves above the guide on smaller screens so the documentation retains the full available width. The QR is rendered from data embedded in `index.html`; it does not depend on a separate image file.

### New task

Opens the task editor with empty fields. The task is not created until **Save task** is pressed.

### Connect Data Folder

Opens the browser folder picker. Select the folder containing `index.html` and all eight expected JSON files. One read/write approval connects the complete dataset and allows **Save Changes** to update every file together. The compatibility file picker can still load all eight files or one combined `dahsiapke_backup.json` in browsers without folder access.

After loading, the automatic archive policy is evaluated.

### Save Changes

In a browser supporting writable directories, requests permission for the connected data folder as the first action from your click, then writes the latest state into all eight files without further file prompts.

In other browsers, downloads one combined backup file. When JSON synchronization is pending, the button is highlighted. The status line independently confirms automatic browser-local persistence.

## 5. Dashboard page

### Active work

Counts incomplete work that is not cancelled, held, or archived.

### Completion

Shows completed active work as a percentage of the current Work Bucket.

### Time invested

Totals logged time from current non-archived datasets.

### Delivery risk

Counts open work that is delayed or at risk.

### Status distribution

Shows the number of current tasks in To Do, In Progress, Review, and Done.

### Delivery health

Summarizes Critical & Important, On Hold, Cancelled, and Review work.

### Work by category

Groups current work by category.

### Upcoming dates

Lists open work with the nearest expected completion dates.

## 6. Work Board page

### 6.1 Work-view buttons

#### Work Bucket

Shows active To Do, In Progress, Review, and Done columns.

#### Critical & Important

Shows open tasks that are important, High priority, delayed, or at risk. Empty workflow columns are hidden.

#### In Progress

Shows only the In Progress board.

#### Done

Shows only active Done work. Done cards are read-only.

#### Work Cancel

Shows cancelled and closed work in a dedicated board.

#### Task On Hold

Shows paused work in a dedicated board.

### 6.2 Filter and sorting controls

#### Priority

Filters cards to High, Medium, Low, or all priorities.

#### Category

Filters cards by one category. Categories found in imported files are included automatically.

#### Importance

Shows all tasks, Important tasks, or Standard tasks.

#### Sort

Sorts visible cards by:

- Priority
- Expected completion date
- Expected start date
- Creation date
- Time spent
- Title

#### Reset

Clears board filters and restores Priority sorting.

### 6.3 Special drop areas

#### Critical & Important

Dragging an active card here marks it important and moves it into focused To Do work.

#### Task On Hold

Dragging a card here pauses it and stores it in the On Hold dataset.

#### Work Cancel

Dragging a card here cancels and closes it.

### 6.4 Workflow columns

- **To Do:** work not yet started
- **In Progress:** work currently being performed
- **Review:** work awaiting verification, approval, or review
- **Done:** completed work

Dragging a card between columns changes its status and dataset. Done cards cannot be dragged.

### 6.5 Card colors

- **Red:** the expected completion date has passed
- **Orange:** completion is within three days and at least 40% remains
- **Normal:** not currently considered delayed or at risk

### 6.6 Card buttons

#### −

Removes 15 minutes from Time Spent. Time cannot become negative.

#### +

Adds 15 minutes to Time Spent.

#### History

Opens Change History filtered to that task.

#### Edit

Opens an active task for editing.

#### View

Opens a Done task in read-only mode.

The task-details window still provides **Delete task** when permanent removal is required.

## 7. Task editor

### Title

Required. A concise name for the work.

### Description

Optional details, acceptance information, expected outcome, or notes.

### Category

Required dropdown. Used by filters, dashboards, and Archive grouping.

### Priority

- **High:** urgent or materially significant
- **Medium:** normal planned work
- **Low:** useful but less urgent

### Status

Select To Do, In Progress, Review, or Done. Saving as Done records `completed_at` and makes the task read-only.

### Progress

An integer from 0 to 100. Done tasks are set to 100 automatically.

### Expected start date

The planned date on which work should begin.

### Expected completion date

The planned date by which work should finish. It cannot be earlier than the expected start date.

### Key reference people

Enter a few relevant names separated by commas, for example:

```text
Aina, Kumar, Farah
```

These may represent sponsors, reviewers, vendors, subject-matter experts, or stakeholders. They are not system users and receive no notifications.

### Parent task

Type part of a task title or category. Select a suggestion to make that task the parent. Search results are limited to a manageable list, so large work collections do not require scrolling through one enormous dropdown.

Use a parent for a project, work package, or phase containing several child tasks.

### Dependencies

Search and add multiple prerequisite tasks. Selected dependencies appear as removable chips.

The application rejects a dependency update that would create a circular path.

### Critical or important

Marks the task for the Critical & Important view.

High-priority, delayed, and at-risk tasks may also appear in that view even when this checkbox is not selected.

### Close

Closes the editor without saving form changes.

### Delete task

Available for an existing active, Done, cancelled, held, or archived task. A confirmation explains whether related parent or dependency references will also be removed.

Deletion performs these operations in the browser-local database:

1. Records a `Task deleted` Change History event.
2. Removes the deleted ID from related dependencies.
3. Clears the deleted ID from child `parent_task_id` fields.
4. Records updates for affected related tasks.
5. Removes the task from its dataset.
6. Marks JSON synchronization as pending.

The deletion is automatically retained locally. After **Save Changes** synchronizes the JSON files, use a previous separate or combined backup to recover it.

### Save task

Validates and saves the task into the automatic local database. A change-history event is recorded. Use **Save Changes** to synchronize the separate JSON files.

## 8. Critical Path page

### Search and select task or parent

Type a task title or category and select a result. Selecting a project parent focuses the analysis on its linked family and dependencies.

### Show overall path

Clears the selected task and calculates the longest dependency sequence across current work.

### Tasks on path

Number of tasks in the displayed dependency sequence.

### Estimated remaining effort

Approximation based on logged effort and incomplete percentage. It is a planning indicator, not a formal resource-loaded schedule.

### Latest expected completion

Latest expected completion date among tasks on the path.

### Dependency sequence

Shows the calculated task order with status, progress, dates, people, and direct prerequisite names.

### Direct dependencies

Shows prerequisites of the selected task. Without a selection, it summarizes the overall path.

### Linked and child tasks

Shows tasks sharing the same parent or directly belonging to the selected parent.

## 9. Archive page

### Automatic archive policy

The policy runs after JSON files are loaded:

1. Sort active Done tasks by `completed_at`.
2. Always keep the three most recently completed tasks in active Done.
3. Archive every other Done task older than three calendar months.

For older Done files without `completed_at`, the application uses expected completion date and then creation date as a fallback.

### Search completed work

Searches active and archived Done records by title, description, category, priority, and reference people.

### Sort

Sorts by newest completion, oldest completion, title, category, or time spent.

### Group

Groups records by:

- Storage: Active Done or Archived
- Category
- Completion year
- Priority

### Archive eligible

Runs the automatic three-month/latest-three policy immediately.

### Archive all active Done

Moves every active Done record into Archive, including the latest three. A confirmation is shown first.

### Archive table

The table shows:

- Work title and description
- Category
- Priority
- Completion date
- Time spent
- Reference people
- Current storage
- Available actions

### Archive action

Moves one active Done task into `archive_kerja.json` in memory.

### Restore action

Moves one archived record back into active Done. If it is older than three months and is not among the latest three, it may be automatically archived again during a future load.

### History action

Opens the audit timeline filtered to that completed record.

### View action

Opens the completed or archived record in read-only mode. From there, **Delete task** can remove unwanted completed work after confirmation, automatic local saving, and JSON synchronization.

## 10. Change History page

Change History begins with changes made by a history-enabled version of the application. Earlier unrecorded changes cannot be reconstructed.

### Filter by task

Searches current and archived task titles and filters the timeline to one task.

### Change type

Filters events such as:

- Created
- Edited
- Status changed
- Completed
- Time changed
- Put on hold
- Cancelled
- Marked critical
- Archived
- Restored
- Deleted

### Show all history

Clears task and event-type filters.

### History summary

Shows the number of matching events, affected tasks, and latest recorded change.

### Timeline event

Each event shows:

- Event type
- Task title at the time of the change
- Date and time
- Source and destination dataset, when relevant
- Changed fields
- Previous and new values

## 11. Help page

The Help page displays the documentation inside dahsiapke.

### Choose document

- **Quick Help:** setup, loading, saving, backup, and troubleshooting
- **Full User Manual:** complete page, button, field, and workflow documentation

The selected Markdown source is rendered as formatted headings, lists, tables, and code blocks. The bundled `help-content.js` file makes both documents available under `file://` without a server or network request. The support QR is generated locally as SVG from an embedded module matrix and does not make an automatic network request.

If `HELPME.md` or `USERMANUAL.md` is changed during application development, regenerate the bundle with:

```text
node tools/build-help-content.mjs
```

Normal users do not need Node.js because the generated `help-content.js` is already included.

## 12. Recommended daily workflow

### Start of session

1. Double-click `index.html`.
2. If they do not load automatically, click **Connect Data Folder** and choose the folder containing all eight files listed in Section 2.
3. Wait for the successful-load message and confirm the Dashboard totals.
4. Review Dashboard and Critical Path.
5. Open Work Board and select Critical & Important.

### During work

1. Move tasks as their status changes.
2. Add time using `+` or remove incorrect time using `−`.
3. Update progress, dates, dependencies, and reference people.
4. Use Task On Hold or Work Cancel when appropriate.
5. Review Change History when previous values are needed.

## 13. Security and operational limitations

- The JSON files are the startup source of truth; IndexedDB is only a browser-specific safety cache during the session.
- Browser security may require one **Connect Data Folder** click after reopening or when permission has expired.
- Clearing browser site data removes the local copy; synchronized JSON files and combined backups remain the recovery mechanism.
- There is no multi-user conflict handling.
- Reference people are labels only; no messages or notifications are sent.
- Native drag and drop may be limited on some mobile browsers.
- The application validates JSON structure, IDs, dates, numeric values, and relationships during import.
- Task content is rendered as text to prevent imported HTML from executing.

## 14. Before closing: synchronize and confirm

Always complete these steps before closing the tab, browser, or laptop:

1. Finish the current edit and close the task editor.
2. Confirm that the storage-status line reports a successful browser safety-cache save.
3. If **Save Changes** is amber or pulsing, JSON synchronization is pending.
4. Click **Save Changes**.
5. If prompted, approve the already connected data folder once; do not select files individually.
6. Wait for the message confirming that all eight JSON files in the folder were updated together.
7. If the browser downloads `dahsiapke_backup.json` instead, confirm that the file finished downloading and retain it as the latest portable backup.
8. Close the application only after either direct synchronization succeeds or the combined backup has downloaded successfully.

Do not assume that the source JSON files are current merely because the browser safety cache is green. **Save Changes** is what synchronizes or backs up the portable JSON data.
