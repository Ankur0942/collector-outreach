# Collector Outreach Ledger

**Live: https://ankur0942.github.io/collector-outreach/**

A single-page tracker for Instagram outreach to collectors. Log every DM you
send, record what came back, and find out which opener is actually earning
replies before you send the next batch.

## What it does

- **Log a contact** — handle, where you found them (unboxing comment, LF/WTB
  post, hashtag), what they collect, and which message variant you used. If
  you've messaged that handle before, it says so and makes you confirm.
- **Track the response** — mark each row replied / not yet / no response, tag the
  objection you hit, and set an outcome (interested, purchased, declined,
  ghosted). Paste their objection verbatim in the note field; it saves as you
  type.
- **See what's working** — reply rate broken out by message variant and by
  source, so the four openers are competing on the record rather than on memory.
- **Read the tally** — logged, sent today, replied, reply rate and purchased,
  plus the objection stamps, all recomputed live.
- **Find things** — search across handles, collects and notes, filter by reply
  status / outcome / variant, sort by date or handle.
- **Get your data out** — export the ledger as JSON or CSV, and import a JSON
  export back (merged by entry id, so re-importing never duplicates).

### Two things it deliberately refuses to do

**It won't count unresolved contacts against you.** Reply rate is
`replied ÷ (replied + no response)`. Someone you messaged an hour ago hasn't
declined to answer yet, so they stay out of the denominator — otherwise every
fresh batch would look like a performance drop.

**It won't crown a winner on thin data.** A variant is only marked `BEST` once
it has at least 5 resolved replies behind it *and* is clearly ahead. Below that
it's labelled `thin data` and the rate is shown in muted grey. One reply from
one send is not a 100% reply rate worth acting on.

## Running it

Use the hosted page at <https://ankur0942.github.io/collector-outreach/>, or
open `index.html` in a browser. No build step, no dependencies, no server.

Entries are saved to `localStorage` under the key `outreach-entries`, so they
persist across reloads but live only in that one browser on that one machine —
clearing site data wipes them, and nothing syncs between devices. The hosted
page and a locally opened `index.html` are separate origins, so they keep
separate sets of entries — pick one and stick with it. **Export to JSON
periodically**; that is the only backup this tool has.

Note: the file is a standalone HTML fragment (styles and script inline, no
`<!doctype>` wrapper), which is why it drops straight into a page or renders on
its own.

## Data shape

Each entry is one object in the `outreach-entries` array:

```json
{
  "id": "1755940000000-k3n1p",
  "createdAt": 1755940000000,
  "handle": "@collector",
  "source": "Comment on unboxing post",
  "collects": "Japanese sealed",
  "variant": "Discovery, no pitch",
  "replied": "Not yet",
  "objection": "None yet",
  "outcome": "Pending",
  "note": ""
}
```

Entries logged before `createdAt` existed still carry their timestamp in the
`id` prefix, and it's recovered from there on load. Imported entries are
validated field by field — anything unrecognised falls back to a safe default
rather than being trusted.

## Guardrails baked in

Keep sends to roughly 20–30/day, and no link in the first message. The
**Sent today** tile counts against that range and turns red when you go over.
