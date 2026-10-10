---
layout: post
lang: en
title: "Toward a Test Suite: Faster Development, Faster Debugging for AliveGR"
date: 2026-10-10 10:00:00 +0000
author: Twilight0
permalink: /en/news/alivegr-test-suite/
---

Something new is in the works for AliveGR: a proper automated test suite. It is not there yet — but it is coming, and it will change how fast this addon gets developed and debugged. Here is why it matters and what it will cover.

## The problem it solves

Greek streaming sites change their markup constantly — sometimes weekly. Historically, finding out meant a user reporting "channel X is down", followed by the slow loop: launch Kodi, click through menus, reproduce, read the log, guess, patch, re-test by hand. And every hurried fix risked breaking two other things, because nothing verified the rest still worked.

A test suite turns that loop from minutes of clicking into seconds of `run and see red or green`.

## What it will cover

* **Scraper regression tests:** saved copies of real site pages as fixtures, so when ERT, MEGA, ANT1 or a VOD portal changes layout, the breakage shows up as a failing test — before release, not after.
* **Resolver and fallback logic:** stream selection, persistent preferences, and silent failover exercised without touching the network.
* **Search and transliteration:** Greek/Greeklish matching (`mega` → `MEGA`, `ερτ` → `ERT`) pinned down so refactors cannot silently break it.
* **Playlist and EPG mapping:** the IPTV Simple Client bridge and channel mapping verified against known-good outputs.
* **No Kodi required:** Kodi's `xbmc` modules get mocked, so the whole suite runs on a plain machine or in CI — no GUI, no box, no Android device needed to catch a regression.

## How it speeds up development

* **Refactor with confidence.** The 3.x modernization touched nearly everything; tests mean the next big cleanup does not rely on luck.
* **CI gates every change.** Break a scraper, and the failure is visible on the commit — not a week later in the issue tracker.
* **Faster triage.** "Channel X is down" becomes: save the page, add it as a fixture, watch the test fail, fix, watch it pass. Reproducible by anyone, not just on the maintainer's setup.
* **Pairs well with the AI workflow.** The machine already handles the boring 80%; a test suite gives it (and me) an instant verdict on every change.

## Status

In the works, landing alongside the 3.0.0 stabilization. If you want to help — fixture pages for broken sources, edge cases, odd markup — open a thread in [GitHub Discussions](https://github.com/Twilight0/plugin.video.alivegr/discussions). The more real-world samples, the stronger the net.
