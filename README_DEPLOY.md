# ERP Dashboard - Sadeq 2026 (v2.2.0)

A single-file web app (`index.html`) for surveillance rating jobs: dashboard, budget vs actual,
year-to-year, dues & aging, follow-ups, renewals, data health, teams, data upload console,
Excel / PDF / print export, backup & restore, activity log.

## 1. Deploy (any static host - no server code, no database)
Copy `index.html` to a web folder and open it in a browser.
- Nginx / Apache / IIS: put it in the site root or a sub-folder.
- GitHub Pages, Netlify, Cloudflare Pages, AWS S3 + CloudFront: upload the file.
- Local only: double-click `index.html`.

## 2. Security - READ THIS
The file itself now contains no business data, but data you upload or enter is stored in the browser
(and, in the published version, in the shared database). Before putting it on a network:
- Put the site behind a login (Basic auth, VPN, SSO / reverse-proxy auth), and use HTTPS.
- Do not publish it on a public URL.

## 3. Libraries (internet needed unless you host them)
The page loads three scripts from cdnjs.cloudflare.com (Excel, PDF export):
- xlsx 0.18.5, jspdf 2.5.1, jspdf-autotable 3.5.31
For an offline / intranet install: download those three files, place them in a `libs/` folder,
and change the three `<script src="...">` lines near the top of `index.html` to `libs/<file>`.
Without them the dashboard still works; only Excel/PDF export and file upload are disabled.

## 4. How data works in standalone mode
- Start-up data = none. The file contains no job or budget data; the dashboard starts empty.
- Control panel > Data console: upload Excel/CSV for Surveillance (jobs), Budget, Dues, Working,
  Year-to-year, and other tables. Use each card's Template button for the expected columns.
- Uploads, notes, follow-ups, teams, status changes and settings are stored in the
  BROWSER (localStorage) of each person/device. They are not shared between users and are lost if
  browser data is cleared. Use Control panel > Backup & restore regularly (the dashboard reminds you
  if the last backup is older than 7 days).
- Team sharing (live shared data between users) is only available in the published
  claude.ai version, not in the standalone file. For a shared multi-user deployment you need a
  small backend (API + database + login); this file can be connected to one later.

## 5. Updating
- New job / budget files: upload through the Data console (per browser), or ask to rebuild
  `index.html` with the new files embedded so everyone starts from the same data.
- Replace `index.html` on the server to ship a new version (check "About & system check" in the
  Control panel for the version).

## 6. Browser support
Current Chrome, Edge, Safari, Firefox (126+ for the page-zoom control). The "About & system check"
card in the Control panel shows which features work on the current device.

## 7. Release notes
### v2.2.0 (2026-10-15)
- Member list rebuilt: the table no longer fills itself from the job data. It starts empty (old members
  are cleared once). Build it by hand, by pasting lines (Name, Department, Team, Role, Phone, Email),
  by uploading an Excel/CSV list, or with "Import analysts from job data".
- New Departments (add / rename / head / delete), Department filter in the top bar, Department table in
  Team report, "Remove all members" (confirm + Undo), members can be grouped by department or team.

### v2.1.0 (2026-10-15)
- Every button is role-aware: buttons a role may not use are greyed out with a tooltip ("Needs Admin ...").
  A "What each role can do" table is in Control panel > My profile & access.
- Command palette (Ctrl/Cmd+K or the Commands button): go to any page, add job, edit budget, upload,
  export, print, zoom, text size, profile, backup - role-gated.

### v2.0.0 (2026-10-15)
- Clean start: all built-in Excel data removed; the dashboard starts empty with an onboarding card.
- Load or change data: Control panel > Data console (upload Excel/CSV for jobs, budget, dues, working,
  year-to-year, other), "+ Add job" on the Jobs page, "Edit job" in a job's side panel (change or delete),
  and "Edit budget" on Budget vs Actual. Changes update every page; Undo is offered.

### v1.4.0 (2026-10-15)
- Sign-in / profile: choose "I am" (your member name). Top-bar view scope: Everyone / My team / Me.
- Roles: Admin, Manager, Member, Viewer (see Control panel > My profile & access).
- My view page: one person's KPIs and jobs next to their team's KPIs and members.
- STANDALONE NOTE: in the standalone file there is no real login. The profile picker only filters what
  is shown; it is NOT a password, and all job data is inside index.html. Use a web-server login/VPN
  for real access control. Real per-user roles need the published claude.ai version (accounts + shared
  database) or your own backend.

### v1.3.0 (2026-10-15)
- Built-in teams "BD Person" and "Other" (Control panel > Team members; also in the team filter).
  "Put all unassigned in Other" assigns everyone not yet placed in a team.
- New Reports > Team report: jobs, agreement, collected, dues, status counts and members per team.

### v1.2.0 (2026-10-15)
- Drag to resize: drag the right edge of any table header to change that column's width (saved per
  device; "Reset column widths" is in each table's Columns menu), drag the sidebar edge to change its
  width, and drag the bottom-right corner of a table box to make it taller or shorter.

### v1.1.0 (2026-10-15)
- Choose which fields show: dashboard summary cards, "Attention needed" cards, dashboard panels, and
  30 optional fields in the Jobs table (Control panel > Fields & display).
- A "Columns" button above every table to show/hide its columns; Excel, PDF and copy exports follow
  the visible columns. Choices are saved per device; reset under Control panel > Reset.

### v1.0.0 (2026-10-14)
Dashboard, budget vs actual with forecast, year-to-year, surveillance status (WIP / Not Done /
Cancel / Halt), working, dues aging, follow-ups, renewals, data health, analysis, column filters,
control panel (teams, colours, size, zoom, resets), data console, activity log, undo, backup &
restore, Excel/PDF/print, keyboard accessibility.
