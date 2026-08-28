# PersianCalendar Data Feed

Remote occasions data for **Roozane (PersianCalendar)** — a Persian/Iranian solar (Shamsi)
calendar app for iOS, watchOS, and iPadOS. Bundle identifier `com.persiancalendar.app`.

App Store listing: **TODO — add link**

## What this repo is

The app fetches `occasions.json` from this repo on every launch, caches it on-device, and
merges it into its bundled baseline holiday/occasion data (`HolidayData.swift`). This means
adding a missing commemorative day, or correcting a wrong date, can ship by editing and
pushing this file — no App Store submission, no waiting on Apple review.

The app **always works fully offline** from its own bundled data first; this feed only adds
to or corrects that baseline. A failed fetch, a malformed file, or no network at all just
means the app keeps showing whatever it already had — it never breaks or shows a blank
calendar because of this feed.

## What's in `occasions.json`

- **`fixedOccasions`** — commemorative days on a fixed Shamsi (solar) month/day every year
  (e.g. national holidays, professional/cultural observance days)
- **`lunarOccasions`** — commemorative days anchored to a Hijri (lunar) month/day, which
  drift ~11 days earlier in the Shamsi calendar each year (mostly Shia religious dates)
- **`gregorianOccasions`** — commemorative days anchored to a Gregorian month/day (mostly
  international observance days), which drift the opposite direction
- **`dateOverrides`** — corrects one specific year's occurrence of a lunar occasion to
  Iran's officially-published Shamsi date, where the app's own tabular-Hijri computation is
  known to drift by a day from the real, government-published calendar

Full field reference: `occasions.schema.md`.

## Where the data came from

- The app's own original bundled dataset (national holidays, Zoroastrian ceremonies,
  commemorative days, religious lunar dates), several of which were independently verified
  against Iran's officially-published calendar (time.ir, bahesab.ir, and other sources)
  where the computed tabular-Hijri date was found to drift by a day from the real one
- A large merge from **[jdf.scr.ir](https://github.com/SCR-IR/Iranian-Calendar-Events)**
  (LGPL v3), a long-established, widely-used Iranian calendar occasions dataset — merged in
  with deduplication against the app's own existing entries

## Editing

1. Edit `occasions.json` directly (or fork + PR)
2. Push to `main`
3. Live within a few minutes — GitHub's raw-content CDN (`raw.githubusercontent.com`) has a
   short cache TTL, after which every app instance picks it up on its next launch

Only entries independently verified against a real source belong here — an entry with a
wrong date is worse than a missing one. See `occasions.schema.md`'s "What NOT to put in
this file" section.

## Access

This repo is public (required — the app fetches the raw JSON anonymously, with no
credentials), but only the repo owner has write access. Public visibility means anyone can
read the file or open a Pull Request; it does not mean anyone can push to `main`.
