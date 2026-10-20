---
layout: post
lang: en
title: "subtitles.gr saga: 4.3.0 and the Android Wall, or How I Learned to Stop Shipping .so Files"
date: 2026-10-20 10:00:00 +0000
author: Twilight0
tags: [subtitles, technical, releases]
permalink: /en/news/subtitles-gr-4-3-0-android-saga/
---

Subtitles.gr 4.3.0 is now available. This is the third post in the saga — after [TLS impersonation](2026-10-09-subtitles-gr-tls-impersonation-and-curl-cffi.md) and [the captcha hand-off](2026-10-18-subtitles-gr-captcha-handoff.md) — and it is the one where Android finally works. What follows is the journey, episode by episode, because the changelog alone does not explain how many times I was wrong before I was right.

## Episode 1: "Does it load curl_cffi?" (it did not)

It started with a log from a Samsung A53: Kodi 21.2, Python 3.11, `script.module.curlcffi v0.16.3 installed` — and every impersonated provider skipping with `needs script.module.curlcffi`. Installed but not loading. My first diagnosis was the `sys.path` gap: Kodi puts the module's bare `lib/` on the path while the importable package sits two levels deeper at `lib/android_arm64-v8a/cp311/`. I fixed that in `impersonate.py` — and the next log said `No module named '_cffi_backend'`. The shipped tree had no cffi backend at all: upstream wheels declare it as a pip dependency, and pip never runs inside Kodi. Desktop only ever worked by accident of the host environment.

## Episode 2: The builder grows a backend (and breaks CI three times)

I vendored `_cffi_backend` on all platforms in the [curl-cffi-builder](https://github.com/Twilight0/curl-cffi-builder): desktop from PyPI wheels per minor, Android/iOS/armv7l cross-compiled from the cffi sdist, plus libffi built from source where the target has none. Along the way I bumped curl_cffi to 0.16.4b1 and impersonate to v2.2.3. CI failed, in order: a missing `-bundle` flag on iOS, a missing `<ffi.h>` everywhere (Xcode doesn't ship it), then `pyconfig.h` missing from CPython source trees (it's generated at build time — I now compile each minor against its own toolcache headers), then `LONG_BIT` errors on both 32-bit targets (64-bit headers meet a 32-bit compiler; patched like the `_wrapper` build already did). Four pushes, all green eventually. I was proud of this. It was all wasted.

## Episode 3: noexec (the one-line experiment that ended it)

With the backend finally vendored, the phone's log gave the real error: `dlopen failed ... not accessible for the namespace`. I copied a binary to emulated storage and tried to execute it: `Permission denied, rc=126`. Android mounts emulated storage `noexec`, and the linker namespace refuses any executable mapping from there. **No native library inside a Kodi addon's tree can ever load on modern Android.** The whole 92MB module, the builder matrix, the CI saga — architecturally impossible on that platform. Not a bug. A wall.

## Episode 4: Gujal00 was right

Around this time [Gujal00 noted on the ResolveURL tracker](https://github.com/Gujal00/ResolveURL/issues/1509) that Kodi 22 (Python 3.14 + OpenSSL 3.x) resolves bot-walled hosts with plain urllib — no modules needed. The gate was never "exact Chrome"; it was "modern client". So I built exactly that, explicitly: a pure-Python transport with Chrome150 cipher order, ALPN, no legacy protocols, and the non-JS User-Agent that already walks past Anubis on its own. I verified the JA3 moves on the wire, then the phone — freshly upgraded to Kodi 22 RC1 — ran the Subs4Series search with zero challenges. curl_cffi stays first choice where it loads; the fallback covers everywhere else. Nothing native, nothing to install, works on every box including the ones that can never dlopen.

## Episode 5: the actual 4.3.0 (bugfixes and small mercies)

With transport settled, I swept the rest:

- **Provider toggles ungated.** The curl_cffi install-checks are gone from Subs4Series, SubDL, Addic7ed and Translate — they stay user-controlled, with a group note on what each setup needs. The runtime already decides per-request; the settings screen finally admits it.
- **One-click Greek.** A new action adds Greek to Kodi's own subtitle language list, keeping existing entries. On a fresh install this replaces the trek through Player → Language → Preferred subtitle language → multiselect dialog. One button.
- **Load local subtitle.** An opt-in entry above the results (only when saving is on, the toggle is on, and kept subtitles exist) opens Kodi's file picker for any `.srt/.sub/.ssa/.ass` and plays it through the normal path.
- **SubZTV non-ASCII crash fixed**, **challenge diagnostics** (Ray ID + egress IP in the log, body dumped for inspection), **Nexus floor** with current module pins.

## The rules of the platform, as I now understand them

For Android: Kodi 22 Piers, period. And curl_cffi is unnecessary on any platform — first choice where it loads, irrelevant where the fallback covers. Older stacks stay on 4.2.0.

Subtitles.gr 4.3.0 is in the Twilight0 repository now.
