# Sandy Plains 8U Softball Lineup Generator

A single-file web app for youth softball coaches to instantly generate a batting lineup and 5-inning fielding rotation for their team.

## Features

- **Enter players one by one**, each with a name and jersey number
- **Save/load your roster** to the browser's local storage so you don't have to re-enter it every game
- **Auto-generates** a randomized batting order and fielding grid that satisfies all rotation rules
- **Persistent Game Info** — date, team names, and field stay visible and editable on both the input and results screens, so a typo doesn't force a regenerate
- **Click-to-swap** any two players in either the batting lineup or the fielding grid
- **Rule validation** with inline error messages — printing is blocked until all violations are resolved
- **PDF export** opens in a new browser tab for printing or saving, with no browser headers or footers
- **Responsive design** — works on desktop, tablet, and mobile
- No installation, no backend, no dependencies to install — just open the HTML file

---

## How to Use

### 1. Enter Game Info
Fill in the game date, home team name, away team name, and the field name (e.g., *Sandy Plains Field 3*). This card stays visible after you generate a lineup, so you can fix any of these fields at any time without needing to regenerate.

### 2. Add Your Roster
Enter each player's name and jersey number individually. Use **+ Add Player** to add rows (6–12 players supported). At 12 players, a Bench position is added to the fielding rotation.

**Save Roster** stores the current roster (names and jerseys) in the browser's local storage, overwriting anything saved previously. **Load Saved Roster** appears automatically whenever a saved roster exists and repopulates the rows from it.

### 3. Generate the Lineup
Click **Generate Lineup** to randomly produce:
- A **batting order** (all players, no duplicates)
- A **fielding rotation** across 5 innings that enforces all rules below

### 4. Adjust if Needed
Click any two rows in the batting lineup to swap them. Click any two cells in the fielding grid to swap those players. Rule violations are flagged in real time.

### 5. Print or Save
Click **Print / Save PDF** to open a clean PDF in a new browser tab. From there, use the browser's native PDF viewer to print or download.

---

## Fielding Rules

The generator enforces the following rules automatically. Manual swaps are validated against the same rules in real time.

| # | Rule |
|---|------|
| 1 | A player cannot play multiple positions in a single inning |
| 2 | A player cannot play the same position more than once across the 5 innings |
| 3 | Every position must be filled every inning |
| 4 | Every player must play an infield position at least **2 times** per game |

---

## Fielding Positions by Player Count

| Players | Positions |
|---------|-----------|
| 12 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field, Left Field, Left Center Field, Right Center Field, Right Field, Bench |
| 11 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field, Left Field, Left Center Field, Right Center Field, Right Field |
| 10 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field, Left Field, Center Field, Right Field |
| 9 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field, Left Field, Right Field |
| 8 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field, Outfield |
| 7 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base, Short Field |
| 6 | Pitcher, Catcher, 1st Base, 2nd Base, Short Stop, 3rd Base |

---

## Running Locally

No build step or server required. Just open the file in any modern browser:

```
open index.html
```

Or double-click the file in your file explorer.

---

## Technical Notes

- **Single file** — all HTML, CSS, and JavaScript is self-contained in `index.html`, including the header icon (embedded as a base64 PNG)
- **Fonts** loaded from Google Fonts (requires internet connection)
- **PDF generation** uses [jsPDF](https://github.com/parallax/jsPDF) and [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable) loaded from CDN (requires internet connection)
- **Roster storage** uses the browser's `localStorage` under the key `sandyPlains8uSavedRoster` — it's local to that browser and device, not synced anywhere
- The fielding grid is generated using a backtracking Latin rectangle algorithm that satisfies the infield minimum rule within a bounded number of attempts, with a cyclic fallback
