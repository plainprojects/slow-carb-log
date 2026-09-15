# slow-carb-log

Anonymous slow-carb diet food log (Sept 14, 2026 – Mar 14, 2027).
Static single-page site, auto-deployed by GitHub Pages on every push to `main`.

Live: https://plainprojects.github.io/slow-carb-log/

## How it works

- **`index.html`** — the entire app. No build step, no dependencies. On load it fetches
  `data/days.json`, then the selected day's JSON, and renders:
  - macro total cards (calories, protein, carbs, fat)
  - meals table (time, items, macros, compliance)
  - hunger table (time, 1–10 level, note)
  - **day timeline** — one SVG chart overlaying hourly steps, the hunger curve,
    meal markers, walk/activity spans, and confounder flags on a shared 5 AM–11 PM axis
  - activity list, compliance checks, day note
  - prev/next day navigation (newest day shown by default)
- **`data/days.json`** — `{"days": ["2026-09-14", ...]}`. Chronological order; the last
  entry is the default view.
- **`data/YYYY-MM-DD.json`** — one file per day. Schema below.
- **`data/_template.json`** — blank day skeleton. Not rendered (name starts with `_`).

## Day JSON schema

```jsonc
{
  "date": "2026-09-14",          // ISO date; must match filename
  "weekday": "Monday",
  "day_number": 1,              // 1-based within the run
  "day_total": 182,
  "totals": {"cal": 1280, "protein_g": 88, "carbs_g": 152, "fat_g": 42, "rough": true},
  "meals": [                    // rows of the meals table; also timeline pills
    {"meal": "Breakfast",        // Breakfast | Coffee | Lunch | Snack | Dinner
     "time": "8:05–8:10 AM",    // free text; timeline uses the FIRST time found
     "items": "description…",
     "cal": 240, "protein_g": 8, "carbs_g": 19, "fat_g": 15,
     "rough": true,             // estimate, not weighed
     "compliance": "Fully compliant"}  // free text; badge-colored by keyword
  ],
  "hunger": [                   // hunger table + amber timeline curve
    {"time": "9:50 AM", "level": 5, "note": "…"}   // level 1–10, or null (e.g. craving w/o number)
  ],
  "activity": [                 // plain list under "Activity"
    {"time": "3:05–3:40 PM", "what": "Outdoor stroll, 35 min"}
  ],
  "events": [                   // timeline overlays (NOT in the tables)
    {"start": "09:50", "label": "decaf coffee", "kind": "coffee"},   // kind: coffee → tan tick
    {"start": "11:25", "label": "no water since breakfast", "kind": "flag"}, // kind: flag → red tick
    {"start": "15:05", "end": "15:40", "label": "35-min stroll", "kind": "walk"} // kind: walk → green span
  ],
  "steps_hourly": [             // blue timeline bars; from Apple HealthKit (iPhone)
    {"hour": 8, "steps": 356}   // hour = 24h local hour bucket
  ],
  "steps_note": "iPhone steps synced through 3:30 PM — evening hours pending.",
  "timeline_insight": "One-line auto takeaway shown under the chart.",
  "compliance_checks": {        // rendered as Pass/Miss badges
    "protein_30g_within_30min": false, "no_white_carbs": true,
    "no_dairy": true, "no_fruit": true, "no_liquid_calories": true
  },
  "note": "Free-text day note shown under the tables."
}
```

Notes for editors:
- All times are **Pacific (America/Los_Angeles)**.
- Hunger scale: **1 = barely hungry, 10 = ravenous**.
- Estimates are the norm: set `"rough": true` and keep the `~` prefix behavior in `index.html`.
- `compliance` badge coloring is keyword-based in `badge()` (`index.html`): contains
  "compliant"/"resisted" → green, "maybe"/"conditional"/"acceptable" → amber,
  "miss"/"not"/"fail"/"craving" → red.
- Meal pills on the timeline map via `MEAL_PILL` in `index.html`
  (Breakfast→B, Coffee→☕, Lunch→L, Snack→S, Dinner→D); unknown names use the first letter.
- Missing sections degrade gracefully: no `steps_hourly` → no bars; no hunger levels → no curve.

## Adding a new day

1. Copy `data/_template.json` → `data/YYYY-MM-DD.json` and fill it in.
2. Append `"YYYY-MM-DD"` to the `days` array in `data/days.json` (keep chronological).
3. Push to `main`. Pages redeploys automatically (usually < 1 min).

## Step data

`steps_hourly` comes from Apple HealthKit synced from the owner's iPhone:

```bash
health-cli query metrics --provider healthkit \
  --start-date YYYY-MM-DD --end-date YYYY-MM-DD \
  --interval hourly --fields step_count
```

Coverage is often partial for the current day (sync lags); record the cutoff in
`steps_note` and leave missing hours out rather than zero-filling.

## Local preview

```bash
python3 -m http.server 8000   # open http://localhost:8000
```

(`file://` won't work — `fetch()` needs http.)

## Anonymity

This repo is **public by design** (free Pages hosting). Rules:

- No real names, emails, addresses, or identifiable details anywhere — in files,
  commit messages, or the rendered page.
- Commit author must use the account noreply address, e.g.
  `329304562+plainprojects@users.noreply.github.com`, never a real email.
- Health-adjacent data (meals, hunger, steps, DEXA-style metrics) is fine;
  identity-linking data is not.
