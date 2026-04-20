# Sandy Plains Softball Lineup Generator

A single-file web app for youth softball coaches to instantly generate a batting lineup and 5-inning fielding rotation for their team.

## Features

- **Paste your roster** in one step, or enter players one by one
- **Auto-generates** a randomized batting order and fielding grid that satisfies all rotation rules
- **Click-to-swap** any two players in either the batting lineup or the fielding grid
- **Rule validation** with inline error messages — printing is blocked until all violations are resolved
- **PDF export** opens in a new browser tab for printing or saving, with no browser headers or footers
- **Responsive design** — works on desktop, tablet, and mobile
- No installation, no backend, no dependencies to install — just open the HTML file

---

## How to Use

### 1. Enter Game Info
Fill in the game date, home team name, away team name, and the field name (e.g., *Sandy Plains Field 3*). The field name appears on the printed PDF.

### 2. Add Your Roster
The **Paste Roster** tab is shown by default. Paste your player list directly — one player per line. The following formats are all accepted:

```
Jane Smith, 12
Bob Johnson 7
Maria Garcia #23
14 Ayla Torres
```

Jersey numbers are optional. After clicking **Import Players**, the roster populates the individual rows for review.

**One by One tab:** Enter each player name and jersey number individually. Use **+ Add Player** to add rows (6–11 players supported).

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
open softball-lineup.html
```

Or double-click the file in your file explorer.

---

## Technical Notes

- **Single file** — all HTML, CSS, and JavaScript is self-contained in `softball-lineup.html`
- **Fonts** loaded from Google Fonts (requires internet connection)
- **PDF generation** uses [jsPDF](https://github.com/parallax/jsPDF) and [jsPDF-AutoTable](https://github.com/simonbengtsson/jsPDF-AutoTable) loaded from CDN (requires internet connection)
- The fielding grid is generated using a backtracking Latin rectangle algorithm that satisfies the infield minimum rule within a bounded number of attempts, with a cyclic fallback
