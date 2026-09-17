# Tech Investment Scan

A private, self-refreshing investment briefing. Hosted on Cloudflare Pages,
locked to one email address, and independent of any chat assistant.

**Live site:** _(add your URL here once step 1 is done)_

## How it works

Three separate jobs, so no single part can take the site down:

| Box | Job | What it is |
| --- | --- | --- |
| Collector | Fetches prices and news on a schedule | A script run by GitHub Actions |
| Writer | Turns raw numbers into briefing prose | Templates, plus an optional AI call |
| Shop window | Shows the finished briefing | `index.html`, this repo |

The collector and writer run on a timer and save their output to a data file.
The website only ever *reads* that file, so the page is never doing live work:
it loads fast, costs nothing to serve, and cannot break while you are reading it.

## Files

| Path | Purpose |
| --- | --- |
| `index.html` | The briefing page itself |
| `_headers` | Response headers Cloudflare applies (no-index, no-cache for data) |
| `robots.txt` | Tells search engines to stay out |
| `SETUP.md` | One-time setup: deploying and putting a login in front of it |

## Build status

This is a plain static site. There is no build step, no framework, and no
dependencies to install — Cloudflare serves the files exactly as they sit
in this repository. Changing the site means editing `index.html` and pushing.

## Roadmap

- [x] **Step 1** — Publish the existing page, privately
- [ ] **Step 2** — Move content out of `index.html` into `data/latest.json`
- [ ] **Step 3** — Collector script on a schedule (prices + news, no AI)
- [ ] **Step 4** — Add the AI commentary, with the page still working if it fails
- [ ] **Step 5** — Archive past editions

## Cost

Hosting and scheduling are free. From step 4, the AI commentary costs roughly
$1-2/month. See `SETUP.md` for the spending cap that keeps it there.
