# NARAKA: BLADEPOINT Event Standings

[中文](README.md) | English

A **single-file, zero-dependency, pure front-end** standings tool for NARAKA: BLADEPOINT events, with a **Chinese / English UI**. Just double-click `index.html` — nothing to install, no internet connection required. The online build can optionally connect to Tencent CloudBase for a public event library and member editing.

## Online

**https://jiestandings.com/**

The live site opens on **Public Events**: a collapsible event history grouped by tag on the left and the live leaderboard on the right. Visitors are read-only, and every public event has its own share link. Click **Local Station** in the top bar (or open `#local`) for your own workspace — events you create or import stay in your browser and are never uploaded.

The public library requires one-time CloudBase setup by the admin; see [Public event library & member editing](#public-event-library--member-editing-optional). Without it, the page is a purely local tool, and opening `index.html` directly goes straight to the Local Station.

## Features

### Formats

- **Points format**: `Total = Placement points + Kill points`
- **Match Point format**: configurable match point threshold (default: Solo 16 / Trios 36) and max matches (default: 8)
  - Live match-point status with a progress bar showing how many points are still needed
  - After activating match point, one more match win automatically crowns the champion
  - **Match point placement bonus**: optional, grows each game after activation (Solo +0.5 / Trios +1)
  - If the match limit is reached with no champion, the highest total wins
  - Configurable whether winning the game that activates match point also counts (the official rule requires *another* win; off by default)

### Match types

- **Survival matches**: placement points + kill points, using the Survival placement table
- **Martial Artist matches**: placement points only, using a separate Martial Artist placement table, with no kill input
- Match type can be switched anytime in the entry screen; a new Solo event defaults its first game to Martial Artist, while a new Trios event defaults to Survival games (you can still switch any game to Martial Artist)

### Maps & weather

- Each game can record a map and weather, shown on the match card and in the leaderboard header tooltips
- **Martial Artist** matches are fixed to one map (shown as Versus-Random in the English UI); **Survival** matches offer 14 variants:
  Morus Isle (Dawn / Midday / Dusk (Fireflies) / Night (Fireflies)),
  Holoroth (Dusk (Fireflies) / Cloudy / Sunny / Starry Night (Fireflies)),
  Perdoria (Eventide (Fireflies) / Midnight (Fireflies) / Morning Dew),
  Wanchu (Sunset / Blaze / Starry Night (Fireflies))
- Variants with fireflies are marked **（虫）** in the Chinese UI (Fireflies in English), so you can tell them apart at a glance
- After creating an event, the first games are pre-filled in order:
  - **Solo**: Game 1 Martial Artist (Versus-Random) → Morus Isle · Dawn → Holoroth · Cloudy → Perdoria · Morning Dew →
    Morus Isle · Midday → Holoroth · Starry Night (Fireflies) → Perdoria · Midnight (Fireflies) → Morus Isle · Night (Fireflies)
  - **Trios**: no Martial Artist game by default — Morus Isle · Dawn → Holoroth · Cloudy → Perdoria · Morning Dew →
    Morus Isle · Midday → Holoroth · Starry Night (Fireflies) → Perdoria · Midnight (Fireflies) → Morus Isle · Night (Fireflies) (7 games)
  - Both modes can switch any game to Martial Artist; games beyond the presets have no automatic map.

### Scoring breakdown

`Total = Carry-in points + Martial Artist match points + Survival match points`

- **Carry-in points**: an optional head-start score per competitor, counted toward the total and toward match point activation
- Carry-in points do not count into single-match scores (match wins are still decided by that game's points)

### Groups (group stage)

- Every competitor belongs to a group (A/B/C…); each game can be limited to specific groups (single / multiple / all)
- The leaderboard can show the merged board or per-group boards; group boards are row filtering + re-ranking — same scoring as the merged board
- Random even splitting, group renaming (all references update automatically), and bulk creation from `[A] TeamName` prefixes

### Region tags

An independent labeling system (separate from groups) for regions, divisions, team ownership, etc.

- Fully custom tag names, each with its **own color** (new tags automatically take an unused color from a 12-color palette; click the swatch to change it anytime)
- The leaderboard gains a "Region" column between **Group** and **Team / Player**, rendered as colored chips (tag color as background, black or white text chosen by contrast); the column hides itself automatically when nobody has a tag
- Each competitor row has a region dropdown; the "Bulk Manage / Delete" dialog can tag many competitors at once
- Tags can be renamed (references update automatically) and deleted (the confirm dialog says how many competitors are affected)

### Scale (8–48 players/teams)

- Bulk paste rosters: one name per line for Solo; `TeamName / Member1 / Member2 / Member3 …` for Trios (separated by `/`, **any number of members**)
  - **Optional line prefixes**: `[A]` for group, parentheses or braces for region — any order, both optional
  - Examples: `[A] (East) TeamName / Member1 / Member2 / Member3`, `{East} PlayerName`, `(East) [A] PlayerName`
  - Accepts half-width and full-width parentheses/braces (4 styles); only line-start prefixes are parsed — parentheses inside names are kept as-is
  - New groups / regions are created automatically and reported in the confirm dialog
- **Bulk manage / delete competitors**: select any number, assign them all to one group (or remove them from groups), or delete in bulk. Groups and region tags can be created right inside the dialog
- **One-click official team rosters**: via "+ Add Official Teams" in the Competitors panel
  - **Trios events**: one row per team (competitor name = team name); members are that team's Trios players + flex players, selectable as MVP right away
  - **Solo events**: one row per player, named `Team.Player` — pick as few as you like, no need for whole teams
  - Toggle between **Official ID** (default, e.g. `成都Wolves.ZK`) and **Chinese nickname** (e.g. `成都Wolves.扎克`)
  - Existing names are skipped automatically; manual entry (bulk paste, row-by-row edits) is unchanged
  - Built-in roster: the 16 teams of **NBPL 2026 Fall Split** (72 players: 17 Solo / 53 Trios / 2 flex); regenerate when the season changes
- The entry grid supports **Enter / ↑ ↓ / ← → keyboard flow** (← → walks across rows through the whole table), unfilled-cell highlighting, jump-to-unfilled, and roster search
- The leaderboard has one column per game showing that game's points only; **the highest score of each game is highlighted automatically**
- The leaderboard **expands fully by default**; with more than 8 rows a "Collapse" button appears, and the lower-right corner can be dragged to resize it manually

### Live standings

- **Display settings** (title-bar button; per-event and exported with the event)
  - **Columns**: toggle visibility, reorder with `←` `→` (or arrow keys once a row is focused, ↑↓ equivalent), set per-column width (empty = auto). `Rank` and `Team / Player` are always shown
  - The "Per game (N columns)" block is managed as a unit: show/hide, move, and set width together
  - **Cells**: vertical padding / horizontal padding / font size sliders, applied live
  - **Rank coloring**: separate rule sets for the Overall board and A/B/C group boards (e.g. gray for ranks 5–8), coloring whole rows; group boards inherit the Overall colors until edited; use “Use Overall Colors” to restore inheritance
  - Fixed layout kicks in only after you change a column width (overflow gets ellipsized); untouched layouts look exactly as before
- **Compact / Full table toggle**: collapses/expands the Carry-in + per-game columns as a unit — handy for streaming and casting
- **Match point champions are pinned to rank 1 immediately**, everyone else shifts down one
- Trios events always count in teams; Solo stays in players

### Match MVP / Martial Artist champion

- **Survival matches** show the MVP of the highest-scoring team
  - Solo: the top scorer themselves
  - Trios: the team name by default; click the chip to pick one of its players → shown as `Team.Player`
  - If a team has no members recorded, the team name is used; tied top scores show "TBD" first — click it to jump straight to the tiebreaker dialog
- **Martial Artist matches** show the "Martial Artist Champion" in the same spot — name only, no player pick
- The MVP stores only "which team + which player"; teams are computed from live scores, so the MVP follows automatically when the top team changes

### Tiebreak rules

Total descending is fixed first; the remaining criteria are editable in Settings → Tiebreak Rules (add / remove, direction, order).

- **Points defaults (Solo)**: Carry-in ascending → Game 1 points ascending → Kill points descending → Highest match score descending → Highest match kills descending → Last game points descending → Last game kills descending → Last game placement ascending
- **Points defaults (Trios)**: Carry-in ascending → Kill points descending → Highest match score descending → Highest match kills descending → Last game points descending → Last game kills descending → Last game placement ascending (no Game 1 points criterion)
- **Match Point defaults**: Carry-in ascending
- If every criterion is equal → tied; order them by clicking names in "Manual Tie Resolution"
- "Clear" removes all criteria (equal totals go straight to tied); "Reset Defaults" restores the defaults for the current mode

### Language (Chinese / English)

- One button at the top right of the top bar switches between the **Chinese and English UI**; your choice is remembered
- First visit follows the browser language: English browsers get English, Chinese browsers stay in Chinese
- Add `?lang=en` (or `?lang=zh`) to a link to force a language — handy for sharing the English version with overseas viewers
- Only UI text is translated; **event names, player/team names, notes and region tags stay exactly as they are**, and exported files are unaffected
  (Maps use in-game English names: 聚窟州 Morus Isle / 火罗国 Holoroth / 龙隐洞天 Perdoria / 宛渠 Wanchu;
  「武道」 renders as "Martial Artist", and its map shows as Versus-Random; weather names like Dusk (Fireflies) / Eventide)

### Misc

- Tie resolution: when a game's top score is tied, a dialog lets you pick which one to highlight (the official tiebreak order is pre-selected)
- When totals are tied and no rule separates them, click names in order in the tie-resolution panel; click again to undo
- End scoring: one click locks the event, disabling all entry operations to prevent accidents; unlock anytime
- Multi-event management; Solo and Trios are fully independent. Events with scoring ended are marked 「🔒已结束」 / 「🔒 Ended」 in the top-bar dropdown
- An empty state on first open (or after deleting everything), with create/import actions right there
- JSON export / import
- Placement tables are editable cell by cell, with built-in official 8-player and 12-player presets

### Bulk event management

Import and bulk management live in the **top bar** (next to "+ New Event"); per-event export / delete stay under Settings → Data:

- **Bulk import**: "Import Events" in the top bar accepts several JSON files at once, then shows one confirm dialog listing all event names. Unreadable files are listed and skipped without aborting the batch; duplicate names get an "(Imported)" suffix
- **Bulk export**: "Bulk Manage Events" in the top bar → tick any number of events, then choose one of two styles:
  - *Export as One File*: packs `{events:[...]}`, restorable in a single import
  - *Export Individually*: one file per event, named after each event
- **Bulk delete**: "Delete Selected" in the same dialog. The confirm lists full event names; deleting everything asks for confirmation again. Deleting the event you are viewing switches to a remaining one automatically
- **Reorder**: drag a row to move it anywhere (great for long distances), or nudge it with the `↑` `↓` buttons at the row end; the top-bar dropdown follows and your selections are preserved

> **About "Export Individually"**: the browser will ask whether to allow multiple downloads — choose **Allow**. Verified working in Edge. If your browser blocks downloads without asking, use "Export as One File" instead.

## Public event library & member editing (optional)

The online build splits into two views:

- **Public Events** (default): event history grouped by tag on the left (searchable, filterable by Solo / Trios) and the live leaderboard on the right. Visitors are read-only, and each event has a share link `#public/<document-id>`.
  - Group headings expand / collapse; the collapsed state is kept in the current browser. An event can belong to multiple tags, so it appears once under each tag with an **Also in: …** note. Use `/` in a tag name to create nested folders, e.g. `NBPL Events/2026 Autumn Split/Stage 2`; legacy tags without `/` stay at the top level.
  - Admins can click **Organize** at the top right of the directory to drag rows or use ↑↓ to reorder events and add / remove tags (new tags can be created inline; every event keeps at least one tag). The result applies to all visitors.
  - The public browse view shows read-only **Match score** cards directly, reusing the match entry card layout. All matches are expanded by default with no height limit, showing the complete entered kills, placement, match score, etc.; clicking a card title still folds that match. The **Collapse ▲ / Expand ▼** button hides or shows the whole section. It appears only in public browse mode — not in edit mode or the Local Station — and never modifies data.
- **Local Station**: your own local workspace. The top-bar **Public Events** button opens the same directory; publishers who pick their own event open it in the station with a **Back to My Events** crumb, while everyone else goes to the read-only public page.
- Local files (`file://`) open the Local Station and never connect to CloudBase.

### Permissions & hidden events

- **Only the publisher can modify a public event's content.** Other approved members are read-only, but can publish their own local events.
- **Admins** can hide / restore / delete any public event, but cannot edit content published by someone else. Admins can still edit events they published themselves.
- **Publishers** can hide / restore / delete their own public events. Other members are read-only and cannot hide or delete someone else's event.
- Viewers without editing permission can open **Display Settings** to inspect the current configuration, but every button and input except **Done** is disabled.
- **Deleting is permanent**: it removes the public event content, tags/order, and hidden state, and all share links stop working. The local copy is kept and is not deleted. Hiding only makes the event invisible to visitors; the data remains.
- **Admins** can also organize any public event's tags and display order. Organizing writes only `tags` and `order` into `published_event_visibility`, never the event body or `rev`, so it cannot conflict with a publisher's autosave.
- "Unpublish" means **hidden but retained**: data stays in CloudBase and can be restored anytime. Visitors no longer see hidden events; publishers and admins find them in the **Hidden** section of the directory.
- Hidden is a UI filter, not strict confidentiality — direct database API reads may still return hidden documents. Do not publish sensitive data.
- Public data lives only in CloudBase and page memory, never in a visitor's localStorage. The browser keeps only a small link map (local event ID → public document ID), not the event body.

### One-time CloudBase setup

1. Register a Tencent Cloud account, complete real-name verification, create a CloudBase environment (Shanghai region), and put its environment ID into `const CLOUD_ENV = ''` in `index.html`.
2. Enable **email verification-code sign-in** under Authentication → Sign-in methods, using the built-in mail service, plus **email password sign-in** and **anonymous sign-in**. Anonymous sessions let visitors read public events; anonymous UIDs are not in the member allowlist and cannot write.
3. Add `jiestandings.com` (and `www.jiestandings.com` if needed) to Environment → Security → Allowed web origins. For local development add `localhost:8123`.
4. Create three collections: `published_events` (content), `published_event_visibility` (hidden state, tags, and ordering), `app_config` (member settings).
5. Set custom security rules on all three (do not use the default "creator only" preset).

   `published_events`:
   ```json
   {
     "read": "auth != null",
     "create": "auth != null && (auth.uid in get('database.app_config.editors').uids || auth.uid in get('database.app_config.editors').admins) && request.data.ownerUid == auth.uid",
     "update": "auth != null && doc.ownerUid == auth.uid",
     "delete": "auth != null && (auth.uid in get('database.app_config.editors').admins || (auth.uid in get('database.app_config.editors').uids && doc.ownerUid == auth.uid))"
   }
   ```

   `published_event_visibility`:
   ```json
   {
     "read": "auth != null",
     "create": "auth != null && (auth.uid in get('database.app_config.editors').admins || (auth.uid in get('database.app_config.editors').uids && request.data.ownerUid == auth.uid))",
     "update": "auth != null && (auth.uid in get('database.app_config.editors').admins || doc.ownerUid == auth.uid)",
     "delete": "auth != null && (auth.uid in get('database.app_config.editors').admins || (auth.uid in get('database.app_config.editors').uids && doc.ownerUid == auth.uid))"
   }
   ```

   `app_config`:
   ```json
   {
     "read": "auth != null",
     "update": "auth != null && auth.uid in get('database.app_config.editors').admins"
   }
   ```

   `published_event_visibility` documents may also store `tags` (an array of tags) and `order` (a number) alongside `hidden`. Old documents without these fields are treated as having the `published_events.folder` value as their only tag — no migration is needed.

6. Create the `app_config` document `_id = "editors"`:
   ```json
   { "uids": [], "admins": [], "names": {} }
   ```
7. Open the deployed page → Member Sign-in: new accounts use **Register**, entering an email and requesting a code first, then setting a password in the next step. Existing accounts sign in with a password. If a password is forgotten, click **Forgot Password** below the password form, verify the email, and set a new password; **Email Code** sign-in is still available. Copy your UID, then add it to both `uids` and `admins`; optionally add a display name under `names`, e.g. `{ "<your-uid>": "Data Team" }`.
8. Sign in again and publish local events via "Bulk Manage Events → Publish to Public Library". Additional members can be approved from the in-page Member Management panel.

> If the library already contains events published before ownership was introduced, backfill `ownerUid` / `ownerName` on each document (publisher UID + display name). Without that, the owner-only update rule leaves those documents uneditable.

> CloudBase trial resources are limited; the personal plan (about ¥19.9/month) is recommended for long-term use.

### Publishing events

Import the files under `赛事数据/` by folder, then select them in **Bulk Manage Events → Publish to Public Library**. In the panel that opens, choose an existing folder or select **+ New folder…** and enter a name or path (use `/` to nest, e.g. `NBPL Events/2026 Autumn Split`), then click **Publish**. That name becomes the event's initial tag; an admin can later change tags and ordering via **Organize** on the public page. Publishing oldest-first keeps groups ordered with the most recently updated first.

- Publishing records your UID as `ownerUid` and shows the publisher name. Local dropdowns and the bulk dialog show the publish state.
- After publishing, the local event and its public record are linked and **sync in both directions automatically**:
  - Local edits (scores, notes, settings, lock, display settings…) upload after about 0.7 seconds; no need to publish again. Other tabs in the same browser refresh immediately; other devices pick changes up by polling in about 10–20 seconds.
  - Editing the same public event in the Local Station updates the local copy (when the local copy is idle and has no unsynced changes).
  - When editing on the public page, changes go to the online record as usual; the local copy pulls them automatically the next time you switch to the Local Station and activate the event.
  - The public page polls for new versions and loads them automatically. While you are typing or have unsaved settings, auto-refresh pauses and shows "A newer version is online".
  - Local dropdowns / the bulk dialog show 🌐 published, hidden, or ⚠️ sync paused.
  - Hidden only affects visitor visibility; publisher edits still sync to the hidden record and appear immediately after restoring it.
- Publishing again still works: it updates the record you published (via the locally stored link or by matching the event ID) and can recreate a deleted online record. Events published by another member under the same ID are never overwritten.
- **If both sides changed**, autosave pauses and reports a conflict. Choose "Load Online Version" or "Keep My Version as a Copy". The copy becomes a new local event without a link; the original receives the online version.
- **If the online record was deleted**, sync pauses, local data is kept, and the state becomes "⚠️ Sync paused". Publish again to create a new record.
- When signed out or on another device, local edits stay in the browser; after signing in as the publisher they sync automatically.

### Sync and permissions

- Visitors who are not signed in automatically get an anonymous session for reading only; anonymous UIDs are not in the allowlist and cannot write. Signing in with email switches to the real account.
- Linked local edits reach CloudBase after ~0.7s; other visitors see them in about 15–20 seconds (10–15 seconds between signed-in members) while the page is visible. Polling pauses when the tab is in the background. Actual timing depends on the network and CloudBase.
- Public events are single-publisher, not collaboratively edited. Content updates use a revision (`rev`) optimistic lock, so conflicts are reported instead of silently overwritten. Hidden state is stored separately and never bumps the content revision.
- Accounts support email + password registration and password sign-in. Registration takes two steps: verify the email, then set a password; resending the code does not clear the password already typed. If a password is forgotten, click **Forgot Password** below the password form, then verify the email, set a new password, and sign in. The reset interface is only reachable through that entry. Old accounts created with verification codes that have no password can also use Forgot Password to set one. **Email Code** sign-in remains available and does not change the password.
- Editing the same local event in multiple tabs of one browser is last-write-wins for localStorage; use one tab while editing. Public writes are still protected by the `rev` lock, and stale tabs get a conflict notice.
- Anonymous sign-in must stay enabled: in the current CloudBase environment, unauthenticated database queries fail with an internal error, so the page uses an anonymous session to read public data. Disabling it makes visitors see a load error.

## Usage notes

1. **Double-check the placement table against the current season's official rules before running an event.** Rules change every season; the built-in defaults (official 8-player: Solo `2.5/1/0.5/0.5`, Trios `4/2/1/1`) are just a starting point — every cell is editable in Settings → Placement table.
2. **Your own data lives in your browser** (localStorage). Switching computers or browsers, or clearing browser data, loses past results — export important events regularly via "Settings → Export Event" or "Bulk Manage Events" in the top bar. Public library data lives in CloudBase and is unaffected by clearing browser data.
3. Single-match ties follow the official order: match total → kills → placement. Damage data is not recorded, so the chain stops there.
4. Click "Save Settings" to apply changes — otherwise they do not take effect. If you switch panels with unsaved settings, the dialog offers: OK = save first, then switch; Cancel = discard the changes and switch right away (coming back shows the saved settings).

## Sample data

Sample data lives in the [`赛事数据/测试数据/`](赛事数据/测试数据) folder — load each file via "Import Events" in the top bar.

- The Stage 1 test data covers three files: Solo Stage 1 Finals, Trios Stage 1 Finals, and Stage 1 Losers Round 2. All later updates are single-day data.

## Local use

Download `index.html` and double-click it in your browser. No server, no build, no internet needed. Local-file mode never connects to CloudBase and hides the public library entry; use the online page for public events.

## Rule sources

Scoring rules are based on the [official NARAKA: BLADEPOINT event page](https://www.yjwujian.cn/match) and the [official rules page for NBPL 2026 Fall Split](https://www.yjwujian.cn/news/match/20260930/37804_1315619.html) — both pages are in Chinese.
