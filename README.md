# PersianCalendar Data Feed

Remote occasions data for the [PersianCalendar](https://apps.apple.com) iOS app. The app fetches
`occasions.json` on launch, caches it locally, and merges it with its bundled baseline data —
so new/corrected commemorative days can ship without an App Store release.

The app always works fully offline from its bundled data; this feed only adds or corrects entries.

## Editing

Edit `occasions.json` and push to `main`. Changes are live within minutes (GitHub's raw CDN
cache TTL) — no app update needed.

See `occasions.schema.md` for the field reference.
