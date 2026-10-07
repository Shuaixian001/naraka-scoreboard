# NARAKA: BLADEPOINT Event Standings

[中文](README.md) | English

A **single-file, zero-dependency, pure front-end** standings tool for NARAKA: BLADEPOINT events, with a **Chinese / English UI**. Just double-click `index.html` — nothing to install, no internet connection required.

## Online

**https://shuaixian001.github.io/naraka-scoreboard/**

Open it and go. Your data is stored in your own browser and never uploaded to any server.

## Features

### Formats

- **Points format**: `Total = Placement points + Kill points`
- **Match Point format**: configurable match point threshold (default: Solo 16 / Trios 40) and max matches (default: 8)
  - Live match-point status with a progress bar showing how many points are still needed
  - After activating match point, one more match win automatically crowns the champion
  - **Match point placement bonus**: optional, grows each game after activation (Solo +0.5 / Trios +1)
  - If the match limit is reached with no champion, the highest total wins
  - Configurable whether winning the game that activates match point also counts (the official rule requires *another* win; off by default)

### Match types

- **Survival matches**: placement points + kill points, using the Survival placement table
- **Martial Artist matches**: placement points only, using a separate Martial Artist placement table, with no kill input
- Match type can be switched anytime in the entry screen; the first game of a new event defaults to Martial Artist

### Maps & weather

- Each game can record a map and weather, shown on the match card and in the leaderboard header tooltips
- **Martial Artist** matches are fixed to one map (shown as Versus-Random in the English UI); **Survival** matches offer 14 variants:
  Morus Isle (Dawn / Midday / Dusk (Fireflies) / Night (Fireflies)),
  Holoroth (Dusk (Fireflies) / Cloudy / Sunny / Starry Night (Fireflies)),
  Perdoria (Eventide (Fireflies) / Midnight (Fireflies) / Morning Dew),
  Wanchu (Sunset / Blaze / Starry Night (Fireflies))
- Variants with fireflies are marked **（虫）** in the Chinese UI (Fireflies in English), so you can tell them apart at a glance
- After creating an event, the first 8 games are pre-filled in order:
  Game 1 Martial Artist (Versus-Random) → Morus Isle · Dawn → Holoroth · Cloudy → Perdoria · Morning Dew → Morus Isle · Midday →
  Holoroth · Starry Night (Fireflies) → Perdoria · Midnight (Fireflies) → Morus Isle · Night (Fireflies)
  (from Game 9 on there are no presets — pick your own)

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
  - **Rank coloring (elimination)**: custom rules (e.g. gray for ranks 5–8) coloring whole rows
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

- **Points defaults**: Carry-in ascending → Game 1 points ascending → Kill points descending → Highest match score descending → Highest match kills descending → Last game points descending → Last game kills descending → Last game placement ascending
- **Match Point defaults**: Carry-in ascending
- If every criterion is equal → tied; order them by clicking names in "Manual Tie Resolution"
- "Clear" removes all criteria (equal totals go straight to tied); "Reset Defaults" restores the above

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
- Multi-event management; Solo and Trios are fully independent
- An empty state on first open (or after deleting everything), with create/import actions right there
- JSON export / import
- Placement tables are editable cell by cell, with built-in official 8-player and 12-player presets

### Bulk event management

Under Settings → Data, alongside the per-event export / import / delete:

- **Bulk import**: "Import Events (multi-select)" accepts several JSON files at once, then shows one confirm dialog listing all event names. Unreadable files are listed and skipped without aborting the batch; duplicate names get an "(Imported)" suffix
- **Bulk export**: "Bulk Manage Events…" → tick any number of events, then choose one of two styles:
  - *Export as One File*: packs `{events:[...]}`, restorable in a single import
  - *Export Individually*: one file per event, named after each event
- **Bulk delete**: "Delete Selected" in the same dialog. The confirm lists full event names; deleting everything asks for confirmation again. Deleting the event you are viewing switches to a remaining one automatically

> **About "Export Individually"**: the browser will ask whether to allow multiple downloads — choose **Allow**. Verified working in Edge. If your browser blocks downloads without asking, use "Export as One File" instead.

## Usage notes

1. **Double-check the placement table against the current season's official rules before running an event.** Rules change every season; the built-in defaults (official 8-player: Solo `2.5/1/0.5/0.5`, Trios `4/2/1/1`) are just a starting point — every cell is editable in Settings → Placement table.
2. **Data lives in your browser** (localStorage). Switching computers or browsers, or clearing browser data, loses past results — export important events regularly via "Settings → Export Event" or "Bulk Manage Events".
3. Single-match ties follow the official order: match total → kills → placement. Damage data is not recorded, so the chain stops there.
4. Click "Save Settings" to apply changes — otherwise they do not take effect. If you switch panels with unsaved settings, the dialog offers: OK = save first, then switch; Cancel = discard the changes and switch right away (coming back shows the saved settings).

## Sample data

Sample data lives in the [`赛事数据/测试数据/`](赛事数据/测试数据) folder — load each file via "Settings → Import Events".

- The Stage 1 test data covers three files: Solo Stage 1 Finals, Trios Stage 1 Finals, and Stage 1 Losers Round 2. All later updates are single-day data.

## Local use

Download `index.html` and double-click it in your browser. No server, no build, no internet needed.

## Rule sources

Scoring rules are based on the [official NARAKA: BLADEPOINT event page](https://www.yjwujian.cn/match) and the [official rules page for NBPL 2026 Fall Split](https://www.yjwujian.cn/news/match/20260930/37804_1315619.html) — both pages are in Chinese.
