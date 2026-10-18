---
layout: post
lang: en
title: "Subtitles.gr 4.2.0: The Captcha Hand-Off, and Why the Human Has to Stay in the Loop"
date: 2026-10-18 20:00:00 +0000
author: Twilight0
tags: [subtitles, technical, releases]
permalink: /en/news/subtitles-gr-captcha-handoff/
---

This is the sequel to [the TLS impersonation post](2026-10-09-subtitles-gr-tls-impersonation-and-curl-cffi.md) — same add-on, the last open case. Subtitles.gr v4.2.0 closes the Subs4Series series downloads that sit behind a **per-request captcha**, and this post is about what shipped, why it is shaped the way it is, and why the shape is not negotiable.

## What 4.2.0 does

When a Subs4Series download answers with a captcha instead of a file, the provider raises the gate and Kodi opens a dialog: QR code, listener address, a three-minute countdown. You open the page on your phone or PC, tick the captcha like a person, and the hand-over carries the resulting archive address back to Kodi, which fetches it with the session your browser just vetted and saves the subtitle. Tested on real downloads — including straight past the site's Anubis check with the handed-over cookies.

The page speaks Kodi's language (Greek Kodi gets the Greek page, anything else English) and leads with the recommended path: a **userscript** served with your address and token baked in — install Violentmonkey once, confirm once, and from then on ticking is enough. The bookmarklet stays as the fallback, then the manual cookie paste. The listener port ships fixed at `50190`, so one install keeps working across runs.

## Why only this shape works

Three facts, all verified, none of them mine to change:

1. **The token is minted per request and answers only the page it was solved on.** Subs4Series' reCAPTCHA key is bound to its own domain, and the token Google issues is bound to the site key *and* the browsing session that solved it. There is no API that mints one, no endpoint that replays one, no server that can stand in for the browser. Kodi has no browser control at all (`xbmcgui` cannot render a page, by design), so no window of ours could ever tick that box.
2. **The file cannot be fetched in advance.** Archives live at `/smp/tmp/<id>_<slug>_<nonce>.zip`, session-free but short-lived — minutes, not hours. Crawling them *is* downloading them, one human captcha per file, so there is no index to build, no mirror to keep, no link worth sharing.
3. **The cookie alone never clears it.** A stored session gets you to the gate faster; it does not open it. Every completed hand-over refreshes the stored session from the browser automatically, so the system heals itself — but the next download can still re-gate, because the site mints a fresh challenge per request whenever it wants one.

Anyone promising fully automatic downloads from behind this gate is either untested or paying a third-party solver farm to pass a human check on their behalf. Which brings us to the other side of the counter.

## Why the administrators stack the layers

Look at it from the operator's chair. A subtitle site lives on **display ads**: every page a human opens renders impressions and pays a fraction of a cent toward bandwidth and hosting. Every archive a bot pulls directly costs bandwidth and server load and renders **zero** impressions. That is not a rounding error — scrapers download in bulk, at machine speed, around the clock, and re-upload elsewhere, where *those* pages earn the ad revenue the original site paid the bandwidth for. It is a straight transfer of money from the operator to whoever runs the bots.

So each layer answers a specific abuse, and they compose deliberately:

* **Cloudflare with TLS fingerprinting** (covered in the previous post) rejects anything that does not handshake like a real browser. This kills the dumb scripts — plain `urllib`, default `ssl`, headless fetchers — before any HTTP is exchanged.
* **Anubis proof-of-work** ("Making sure you're not a bot") puts a CPU toll on every request. A human pays it once and never notices; a scraper making ten thousand requests pays it ten thousand times. It taxes automation without blocking people.
* **A per-request captcha** demands proof of humanness *per action*, not per visit. It cannot be stockpiled, shared, or solved once and replayed — the token dies with the request. This is the layer that ends every "clever client" design, because there is no client-side cleverness that manufactures a human.
* **Expiring archive URLs and rotating sessions** kill redistribution. Even a solved download cannot become someone else's permanent link five minutes later.

None of this is spite, and none of it is aimed at Kodi users. It is survival math: without the layers, the bots eat the margin and the site dies; with them, humans pass through and machines pay or leave. Every bypass wave in this arms race has historically bought a harder gate — Enterprise challenges, score thresholds, IP bans — which is why "clever" automation against a small community site is not victimless. It poisons the well for the manual path too, including yours.

## The caveats, stated plainly

* **The tick stays.** It is the site's price of admission, and nothing here defeats, bypasses, or pays to ignore it. The code only transports the result of a check you passed yourself.
* **Three minutes, LAN-only.** The dialog waits 240 seconds and the page answers only inside your own network. A forgotten dialog holds a port; cutting a user off mid-captcha costs the download. The trade was made consciously.
* **One install up front.** Violentmonkey (or the bookmarklet) once, then ticking is the whole job. Clearing the import token rotates the secret and kills every helper made before it.

## What I will not build

Solver services (CapSolver and kin) would technically close the loop: extract the sitekey, buy a token, submit server-side. I am not doing it — not as a feature, not as an option. Beyond the operational drag (a paid key, a balance to feed, per-download billing on a subtitle add-on), it pays someone else to manufacture the exact proof the site demands from *you*, and the escalation it invites lands on everyone using the manual path. The human stays in the loop. That is the project rule, and this release is built around it instead of around it.

## How to use it

1. Play an episode, open **Subtitles → Download**, pick a Subs4Series result.
2. When the QR dialog appears, scan it (or press **Open in browser** on the same machine).
3. First time only: install Violentmonkey, then the helper from the page's install link.
4. Tick the captcha on the subtitle page. The subtitle lands in Kodi.

Subtitles.gr 4.2.0 is in the Twilight0 repository now.
