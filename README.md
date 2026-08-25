# LO*OP Center — Catalog Entry App

A mobile-friendly web app for entering new items into a shadow copy of Liza Loop's
HCLE catalog database. Entries are saved as small JSON files in this GitHub
repository, so every device shares one list and one IdNum sequence. The Export tab
generates `INSERT` statements matching the `catalog` table, ready to paste into
phpMyAdmin on Liza's system.

## One-time setup (about 5 minutes)

### 1. Create the repository
On github.com: **New repository** → name it (e.g. `loop-center-entry`) → **Public**
(required for free GitHub Pages) → Create.

### 2. Upload the app
On the new repo's page: **Add file → Upload files** → drag in `index.html` and this
`README.md` → Commit.

### 3. Turn on GitHub Pages
Repo **Settings → Pages** → under "Build and deployment" choose
**Deploy from a branch**, branch `main`, folder `/ (root)` → Save.
After a minute or two the app is live at
`https://<your-username>.github.io/loop-center-entry/`.

### 4. Create an access token (lets the app save entries)
GitHub **Settings → Developer settings → Personal access tokens → Fine-grained
tokens → Generate new token**:
- Repository access: **Only select repositories** → pick this repo
- Permissions → Repository permissions → **Contents: Read and write**
- Expiration: your choice (you can regenerate later)
Copy the token (starts with `github_pat_`).

### 5. Configure each device
Open the app URL on the phone/tablet, go to **Settings**, and enter:
owner (your GitHub username), repository name, the token, and your cataloger
initials. Tap **Test**, then **Save settings**. Done — that device is connected.

## Daily use
- **New entry**: fill in the form, tap Save. The app assigns the next free IdNum
  (starting at 3209, continuing after the Aug 2026 export) and shows it big so you
  can label the physical item. "New similar" starts the next entry with
  maker/condition/location fields kept.
- **Batch**: everything saved so far, newest first. Tap an entry to edit it.
- **Export**: builds the SQL `INSERT` for all entries in the batch — copy it or
  download `loop_center_new_entries.sql`, then paste into phpMyAdmin's SQL tab on
  `lizaloop_HCLEcatalog`.

Two devices can work at the same time; if both save at the same moment, the app
detects the ID collision and takes the next free number automatically.

## Notes
- The repository is public, so the entry data in `data/entries/` is publicly
  visible. Don't enter anything private. The token is NOT in the repo — it lives
  only in each device's browser.
- After a batch is uploaded to Liza's system, the `data/entries/` files can be
  moved to an `uploaded/` folder in the repo (or deleted) to start a fresh batch —
  set "First IdNum" in Settings to the next number so the sequence continues.
- The form covers the hardware field set; other item types (books, magazines,
  photos, software) can be added as new modes later.
