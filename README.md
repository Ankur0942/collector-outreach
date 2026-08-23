# Collector Outreach Ledger

**Live: https://ankur0942.github.io/collector-outreach/**

A single-page tracker for Instagram outreach to collectors. Log every DM you
send, record what came back, and read the tally before you send the next batch.

## What it does

- **Log a contact** — handle, where you found them (unboxing comment, LF/WTB
  post, hashtag), what they collect, and which message variant you used.
- **Track the response** — mark each row replied / not yet / no response, tag the
  objection you hit, and set an outcome (interested, purchased, declined,
  ghosted). Paste their objection verbatim in the note field.
- **Read the tally** — the stats row (logged, replied, reply rate, purchased) and
  the objection stamps both recompute live from your entries, so the most common
  objection is always visible at the top.

## Running it

Use the hosted page at <https://ankur0942.github.io/collector-outreach/>, or
open `index.html` in a browser. No build step, no dependencies, no server.

Entries are saved to `localStorage` under the key `outreach-entries`, so they
persist across reloads but live only in that one browser on that one machine —
clearing site data wipes them, and nothing syncs between devices. The hosted
page and a locally opened `index.html` are separate origins, so they keep
separate sets of entries — pick one and stick with it.

Note: the file is a standalone HTML fragment (styles and script inline, no
`<!doctype>` wrapper), which is why it drops straight into a page or renders on
its own.

## Guardrails baked into the footer

Keep sends to roughly 20–30/day, and no link in the first message.
