---
layout: post
lang: en
title: "Subtitles.gr Under the Hood: Dead Providers, TLS Impersonation, and curl_cffi"
date: 2026-10-09 19:00:00 +0000
author: Twilight0
permalink: /en/news/subtitles-gr-tls-impersonation-curl-cffi/
---

A few additional, more technical words about Subtitles.gr v4.0.0 — specifically about which providers survived, why two of them are disabled by default, and what `curl_cffi` has to do with any of it.

## What survived, what didn't

Bluntly: the original providers are gone. Only the name remained (and the language).

* **Works out of the box:** Subs4Free, GreekSubs.net, YIFI, TVsubtitles.net, Moviesubtitles.org.
* **Retired:** Vipsubs.gr, Xsubs.tv, Podnapisi.net — dead sites, removed.
* **Disabled by default:** the `subtitles.gr` domain itself (it does not load, its scrapers were not updated), plus SubDL and Subs4Series — for a more interesting reason, below.

## Why SubDL and Subs4Series need a "hack"

Those two sites' servers demand **TLS fingerprinting with advanced HTTP behavior**: they inspect the client's TLS ClientHello (cipher suites, extensions, ordering — the JA3 signature) and reject anything that does not look like a real browser. Plain `urllib` — or anything built on Python's `ssl` module with default settings — fails the handshake check before any HTTP is even exchanged.

The fix has a name: [curl_cffi](https://github.com/yifeikong/curl_cffi) — Python bindings for a patched curl (curl-impersonate) that reproduces real browser fingerprints at both the TLS and HTTP/2 layers. With impersonation enabled, the servers see "Chrome" instead of "a Python script" and serve the subtitle downloads normally.

## The build problem: shipping native code to Kodi

`curl_cffi` is not pure Python — it wraps a compiled native library. Kodi targets have no compiler, and the Twilight0 repository serves everything from Linux desktops to LibreELEC boxes to Android (FireTV, Shield, phones) with all its quirks: multiple ABIs (`arm64-v8a`, `armeabi-v7a`, `x86_64`), NDK toolchains, API levels.

So for this to work I had to construct **builder scripts and prebuilt Python wheels** — "recipes" that compile the native code per platform, so each device downloads a matching binary instead of building from source. Android, with its many quirks, was the hard part.

## How to enable them

SubDL and Subs4Series stay opt-in deliberately — most users never need them, and the native dependency is heavy. To turn them on:

1. Open the Subtitles.gr addon **Settings → Actions → Install curl_cffi** and let the matching wheel install.
2. Toggle SubDL and Subs4Series to the **enabled** state in the provider list.

Everything else — Subs4Free, GreekSubs, YIFI, TVsubtitles.net, Moviesubtitles.org — needs nothing and works immediately after installing the addon from the Twilight0 Repository.
