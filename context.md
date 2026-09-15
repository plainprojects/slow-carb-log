# context.md — who this log is for and how to read it

> Anonymity rule: this repo is public. No real names, emails, addresses, or
> identity-linking details anywhere. The owner is "the owner"; family members
> are referenced by role only.

## The owner

- Male, 48, 72" tall. Sedentary desk job; no smartwatch — all step data comes
  from his iPhone's motion chip, so steps register only when the phone is on
  his person (hand, pocket, armband). Phone left at the desk = missing steps.
- Owns Tonal strength-training equipment at home (workouts may or may not sync
  to Apple Health — treat lifting as manually reported).
- Timezone: America/Los_Angeles. All times in the data files are Pacific.

## Baselines (DexaFit Seattle, DEXA)

| Date | Total | Body fat | Fat mass | Lean mass | Visceral fat |
|---|---|---|---|---|---|
| 2019-12-18 | 187.0 lbs | 24.9% | 46.9 lbs | 134.8 lbs | 1.38 lbs |
| 2021-08-05 | 172 lbs | 19.4% | ~33.4 lbs | 132 lbs | 0.93 lbs |
| 2022-06-02 | 174 lbs | 20.6% | ~35.8 lbs | 132 lbs | 0.81 lbs |
| 2026-03-13 | 203.6 lbs | 31.3% | 63.8 lbs | 132.9 lbs | 2.77 lbs |

Key facts:
- Lean mass has been rock-steady (~132–135 lbs) across all four scans. The ~30 lb
  gain from Jun 2022 → Mar 2026 is essentially all fat.
- Visceral fat tripled since 2022 (0.81 → 2.77 lbs); it typically comes off early.
- He has been at target before: 172 lbs / 19.4% (Aug 2021) and 174 lbs / 20.6% (Jun 2022).
- Next scan: ~March 2027 (end of diet). Never book anything without asking.

## Goals (set Sept 13, 2026)

- Weight: 203 lbs → 170–180 lbs
- Waist (relaxed, at navel): 36" → 34" trousers (stretch: 32")
- Body fat: 31.3% → ≤20%
- Friday check-ins: weight + waist, mornings preferred.

Math note: at ~133 lbs lean mass, 20% body fat ≈ 166 lbs total. Hitting 20% at
175 lbs would require gaining ~7 lbs of lean mass via resistance training.

## The diet

Tim Ferriss's **slow-carb diet**, strict/original rules — Ferriss's own rules are
the authority over community interpretations. Six-month run: **Sept 14, 2026 –
Mar 14, 2027**.

Standing food rules:
- Max **2 eggs per person per day**.
- Vegetarian food at home; meat/fish only at restaurants.
- Avoid: paneer, curd, cheese, yogurt, milk, grains, fruit, liquid calories.
- Accepted exceptions: unflavored lactose-free whey, ghee, ≤2 tbsp cream in coffee.
- **Saturdays are cheat days** — always logged as compliant.
- Zero shame for weekday slips; the rule is "return to slow-carb at the next meal."

Festival days: on Indian festival days he avoids meat and eggs (he flags the
dates himself — do not assume). Protein those days comes from legumes/dal/whey/soy.

## Home & cooking dynamics

- His wife often jumps in and cooks despite his goal to cook himself. She is a
  proficient cook who wings it — exact measurements and full ingredient lists are
  frequently unavailable.
- **Estimate from photos + descriptions, mark everything rough, never badger for
  precision.** Consistency of logging over weeks beats single-meal precision.
- Cooking rhythm: alternate nights — cook every other evening, ~2 days of food
  per session, nothing refrigerated more than ~2 days. (The "cook once on Sunday"
  model was rejected.)
- His wife's constraints (she may join later; she does not use a written plan):
  natural protein sources, dislikes processed food, prefers variety.
- Family eats vegetarian at home.

## Input style

- **Photos first.** When measurements aren't available (which is often), he sends
  photos of the plate plus whatever description he can. Estimate portions from
  the photo and say what you're assuming.
- **Free-form text.** "Had rajma and cauliflower", "ate pizza last night" —
  parse it, don't interrogate it.
- **Hunger readings are a first-class signal, not metadata.** He wants them
  tracked diligently: pre-meal hunger on the 1–10 scale with as many meals as
  possible, plus notable spikes or cravings between meals with timestamps.
- **Timestamps matter.** Meal start/finish times, coffee time + regular/decaf —
  the timeline analysis depends on them.

## How data gets into this log

- He texts free-form meal updates + photos in chat; an assistant parses them,
  estimates nutrients, and writes the day JSON.
- Each meal records start/finish times and a **1–10 hunger level**
  (1 = barely hungry, 10 = ravenous), ideally pre-meal.
- **Coffee is logged with time + regular/decaf** — it suppresses hunger and is a
  confounder, not a meal.
- Post-meal walks/strolls come from Apple Health's hourly step buckets
  automatically; **lifting must be reported manually** (steps don't capture it).
- Watch for confounders and log them (dehydration, poor sleep, stress) — they
  explain hunger better than willpower does.

## Compliance rulings so far

| Food | Ruling |
|---|---|
| Unflavored whey (e.g. Puori PW1) | Compliant |
| Ascent flavored whey | Maybe — acceptable in practice; unflavored is stricter |
| OWYN 32 Pro Elite RTD (32g protein, zero sugar) | Maybe — practical emergency option; flavored/processed |
| IQBAR Chocolate Sea Salt | Not compliant — processed protein bar / domino food; lesser evil than granola in a genuine emergency only |
| MadeGood Organic Granola Bites | Not compliant — grain-based; gluten-free/organic doesn't change that |

New foods: rule on them in the same Compliant / Maybe / Not-compliant frame and
append to this table.

## What he's trying to learn (analytical goals)

This isn't just a ledger — he wants patterns surfaced:

- **Activity ↔ hunger:** does a morning walk blunt the late-morning spike? Do
  high-step days show flatter hunger curves? The day timeline exists for this —
  read the hunger curve against the step bars first.
- **Protein timing ↔ satiety:** does hitting protein early change afternoon hunger?
  Does the missed 30g-within-30-min rule show up in the 11 AM reading?
- **Confounders:** dehydration, poor sleep, stress, coffee timing — log them; they
  often explain hunger better than the food does.
- When you spot a plausible pattern, say so concretely with the numbers. That's
  the "thinking partner" job, not just data entry.
- **Protein is the headline metric** when summarizing a day. Calories are
  informational, never targets.
- Streaks and honesty over perfection. This log is a thinking partner's
  instrument, not a report card.
