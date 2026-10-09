---
layout: post
title: "Twilight0 Repository Updates"
date: 2026-10-09 10:00:00 +0000
author: Twilight0
---

A massive wave of updates is now available in the Twilight0 Repository for Kodi 20 (Nexus) & 21 (Omega)!

---

## 📺 AliveGR (3.0.0~beta1 – 3.0.0~beta3)

The flagship Greek streaming add-on has undergone a major modernization and feature overhaul:

* **IPTV Simple Client Integration**: Full automated bridge to configure `pvr.iptvsimple` with multi-instance support (instance presets), generating an optimized M3U playlist with native `inputstream.adaptive` manifest and stream headers.
* **Greek XMLTV EPG Integration**: Automated setup with Greek EPG guide feed (`https://ext.greektv.app/epg/epg.xml.gz`) and comprehensive channel mapping.
* **Channel Zapping**: Live TV lineup populates into the playlist for seamless previous/next channel switching.
* **Per-Stream DRM & Header Support**: Per-stream schema for live TV with individual ClearKey DRM licenses and HTTP header pairs, fixing streams like Mega and others requiring specific user-agents/tokens.
* **Stream Selector & Preferences**: "Choose Stream" context menu with persistent stream preferences and silent fallback if a stream fails.
* **Fixed Playback Repeat Issue**: Completely removed automatic `PlayerControl(RepeatAll)` toggles that caused single videos in YouTube and AliveGR series to loop indefinitely; added a dedicated repeat mode toggle in Developer settings with Greek and English translations.
* **Greek-Movies Host Fixes**: Resolved parsing errors on grouped episode links.
* **Modernized Core**: Dropped obsolete Python 2 compatibility code, removed the localhost proxy in favor of PluginsGR, removed the heavy M3U8 dependency, and streamlined artwork/logos to fetch dynamically with caching.

---

## 💬 Subtitles.gr & Global Context Menu (v4.0.0)

The dedicated Greek subtitles provider for Kodi returns completely revamped:

* **Brand New & Restored Providers**: Added Subs4Free (with custom user-agent for movies), GreekSubs.net, YIFI, TVsubtitles.net, and Moviesubtitles.org.
* **Cleaned Up Dead Sites**: Removed Vipsubs.gr, Xsubs.tv, and Podnapisi.net; disabled unreachable Subtitles.gr domain by default.
* **Accurate Search Matching**: IMDb ID integration passed directly to providers that support it, plus fuzzywuzzy title matching and updated layout scrapers.
* **Global Context Menu Companion** (`context.subtitles.gr`): Quick subtitle download directly from any Kodi library item or file listing.
* **Modern Stack**: Fully ported to Tulip 4.x, modern parsers, unicache, and native Python 3.

---

## 📻 E-Radio.gr (v4.0.0)

The premier Greek radio station add-on is completely modernized compared to older 2.x/3.x versions:

* **HTTPS Migration & Stream Fix**: All endpoints, artwork, and station streams migrated to HTTPS, respecting `liveProtocol` to fix playback failures.
* **Encoding & Display Fixes**: Enforced UTF-8 decoding to stop Greek station labels from getting stripped or corrupted.
* **Pruned Broken Feeds**: Removed broken "Developer's picks" feed that was causing listing crashes and search errors.
* **Search & Cache Improvements**: Enhanced fuzzy search with duplicate handling and versioned function caches so station lists stay fresh without serving stale data.
* **Modern Stack**: Built on Tulip 4.x, urldispatcher, and unicache with Python 3 reuse language invoker for fast loading.

---

## 🎵 SomaFM (v4.0.0)

Major leap forward from previous 2.x/3.x releases:

* **Clean JSON API**: Replaced legacy, brittle `channels.xml` parsing with the modern SomaFM HTTPS `channels.json` API.
* **Robust Stream Resolution**: Resolves streams directly by station ID instead of passing serialized Python lists inside URLs; fixed lowest-AAC quality selecting the wrong playlist.
* **Real-time Song History**: Localized track history table displaying play times formatted to your local timezone.
* **Instant Cache Invalidation**: Refreshing now clears the listing cache first to always show current "Now Playing" tracks.
* **Lightweight**: Dropped external `html2text` dependency in favor of standard library parsing.

---

All add-ons are available directly from the **Twilight0 Repository** (`repository.twilight0-2.0.2.zip`).
