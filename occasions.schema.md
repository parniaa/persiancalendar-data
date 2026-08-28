# occasions.json field reference

Top-level object:

```json
{
  "schemaVersion": 1,
  "updatedAt": "2026-08-28",
  "fixedOccasions": [ ... ],
  "lunarOccasions": [ ... ],
  "dateOverrides": [ ... ]
}
```

- `schemaVersion` — bump only if the *shape* of this file changes in a way older app
  versions can't parse. The app ignores a file whose `schemaVersion` it doesn't recognize
  and falls back to bundled data, so old app installs never crash on a newer schema.
- `updatedAt` — informational, `YYYY-MM-DD`, for humans skimming the file/git history.

## fixedOccasions

A commemorative day that occurs on the **same Shamsi month/day every year**.

```json
{
  "id": "cooperation-day",
  "name": "روز تعاون",
  "description": "سیزدهم شهریور، روز تعاون",
  "month": 6,
  "day": 13,
  "category": "observance",
  "isDayOff": false
}
```

- `id` — stable slug, unique across this whole file and never reused for a different
  occasion once published (the app keys on it; changing it makes the app treat it as a new entry).
- `category` — one of: `national`, `religiousShia`, `religiousSunni`, `cultural`, `ceremony`, `observance`.
- `isDayOff` — `true` only for actual official public holidays. Almost everything added
  here should be `false`.

## lunarOccasions

A commemorative day anchored to a **Hijri month/day** (shifts ~11 days earlier in the
Shamsi calendar every year). The app computes the Shamsi date itself via its tabular-Hijri
conversion — do not put a Shamsi date here.

```json
{
  "id": "example-lunar-day",
  "name": "...",
  "description": "...",
  "hijriMonth": 1,
  "hijriDay": 9,
  "category": "religiousShia",
  "isDayOff": false
}
```

## dateOverrides

Corrects a *specific occurrence* of a lunar occasion (either one already bundled in the
app, or one defined in `lunarOccasions` above) to Iran's officially-published Shamsi date,
where the app's tabular-Hijri computation is known to drift by a day.

```json
{
  "id": "arbaeen-h1448",
  "year": 1405,
  "month": 5,
  "day": 13
}
```

- `id` here must match `"<slug>-h<hijriYear>"` — the same convention the app's bundled
  overrides use. Only add an entry once you've independently verified the official date
  against at least one real source (see the app's commit history / memory notes for the
  verification process used so far).

## What NOT to put in this file

- Official public holidays that shift the app's core behavior in ways that need testing
  (new Eid dates, etc.) — those still belong in an app update, reviewed and tested first.
- Anything unverified. An entry with a wrong date is worse than a missing entry.

## gregorianOccasions

An occasion anchored to a **Gregorian month/day**, recurring every Gregorian year (e.g.
international observance days). Not yet consumed by the app — the Swift side needs a
Gregorian→Shamsi conversion path added before these can be displayed. Kept here so the
data isn't lost while that's pending.

```json
{
  "id": "jdf-miladi-1-1-0",
  "name": "آغاز سال میلادی",
  "description": "آغاز سال میلادی",
  "gregorianMonth": 1,
  "gregorianDay": 1,
  "category": "observance",
  "isDayOff": false
}
```
