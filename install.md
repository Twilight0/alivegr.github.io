---
layout: default
title: Install & FAQ
description: How to install AliveGR on Kodi via the Twilight0 repository or direct zip, recommended setup, compatibility and frequently asked questions.
permalink: /install/
---

<div class="post">
<div class="post-content" markdown="1">

## Install &amp; FAQ

Everything in one place: installation (taken from the [plugin.video.alivegr README](https://github.com/Twilight0/plugin.video.alivegr/blob/master/README.md)), recommended setup, compatibility, and answers to common questions.

<div class="install-toc" markdown="1">
**On this page:** [Installation](#installation) · [Recommended configuration](#recommended-configuration) · [Compatibility](#compatibility) · [FAQ](#faq) · [Support](#support)
</div>

## Installation

### Method 1: Via Twilight0 Repository (Recommended)

Installing via the repository ensures all dependencies, resolvers, and future updates are installed automatically:

1. In Kodi, navigate to **Settings** (gear icon) → **File Manager** → **Add source**.
2. Select `<None>` and enter the following URL:
   ```text
   https://twilight0.github.io/repository.twilight0/
   ```
3. Enter a name for the media source (e.g. `Twilight0 Repo`) and click **OK**.
4. Go back to Kodi's home screen, click **Add-ons** → **Add-on browser** (open box icon at top left).
5. Select **Install from zip file** (enable *Unknown sources* in Kodi settings if prompted).
6. Select `Twilight0 Repo` and click `repository.twilight0-2.0.zip`.
7. Once the repository is installed, select **Install from repository** → **Twilight0 Repository** → **Video add-ons** → **AliveGR** → **Install**.

### Method 2: Direct Zip Download

You can also download the repository ZIP file directly:

* Repository ZIP: [repository.twilight0.zip](https://raw.githubusercontent.com/Twilight0/repository.twilight0/gh-pages/repository.twilight0.zip)

After downloading, in Kodi go to **Add-ons** → **Add-on browser** → **Install from zip file** and select the downloaded file, then continue from step 7 above.

## Recommended configuration

For the best streaming experience:

1. Ensure **InputStream Adaptive** is enabled:
   * Kodi **Settings** → **Add-ons** → **My add-ons** → **VideoPlayer InputStream** → **InputStream Adaptive** → **Enable**.
2. In AliveGR Add-on Settings:
   * **Streams**: Leave *Live TV Stream Switcher* on `Adaptive` or `Best` according to your bandwidth.
   * **Appearance**: Choose your preferred Icon Theme (`Gemini` recommended).
   * **Folders**: Toggle off any categories you do not use for a cleaner root menu.

## Compatibility

* **Tested Kodi versions:** 20 (Nexus), 21 (Omega), 22 (Piers — in progress).
* **Supported platforms:** Linux (Garuda / Arch, Debian / Ubuntu, LibreELEC, CoreELEC), Android / Android TV / Google TV (FireTV, Nvidia Shield, smart TVs, mobile), Windows (x86_64), macOS / iOS / tvOS.
* **Key requirements:** [inputstream.adaptive](https://github.com/xbmc/inputstream.adaptive) (Kodi built-in binary addon, required for HLS/DASH and DRM playback), plus dependencies auto-installed via the Twilight0 repository (tulip, ResolveURL + PluginsGR, unicache, netclient, scrapetube, AliveGR artwork).

## FAQ

<details class="faq" markdown="1">
<summary markdown="span">Which install method should I use?</summary>

Use **Method 1 (repository)**. It pulls in all dependencies and keeps AliveGR updated automatically. Use the direct zip only if you cannot add a file source in Kodi.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Kodi asks about "Unknown sources". Is that normal?</summary>

Yes. Kodi shows this when installing from a zip file. Enable it when prompted (Kodi settings), install the repository zip, and you can leave it on or turn it back off afterwards.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Which Kodi versions and devices work?</summary>

Kodi 20 and 21 are tested; Kodi 22 support is in progress. Linux, Android / Android TV / Google TV, Windows, macOS / iOS / tvOS are supported — including LibreELEC / CoreELEC boxes, FireTV / Shield, and mobiles.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Do I need InputStream Adaptive / Widevine?</summary>

Yes, make sure **InputStream Adaptive** is enabled (see above). DRM-protected streams need Widevine, which Kodi pulls in via InputStream Adaptive on first use. Without it, HLS/DASH and encrypted channels will fail.
</details>

<details class="faq" markdown="1">
<summary markdown="span">A channel won't play, buffers, or says geo-restricted. What now?</summary>

AliveGR tries fallback streams automatically. If one fails, try the **"Choose Stream"** context-menu entry on the channel to pick another feed, or switch the *Live TV Stream Switcher* between `Adaptive` and `Best` in settings. Some sources are geo-blocked outside Greece/Cyprus — that is a source restriction, not a bug.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Adaptive vs Best stream switcher — which one?</summary>

`Adaptive` adjusts quality to your bandwidth (best for slower or unstable connections). `Best` always tries the highest quality. Start with `Adaptive` unless you know you have plenty of bandwidth.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Search doesn't find my channel. Any tricks?</summary>

Search covers Live TV, Movies, Series, Shows, Theater and Animation, and Live TV search understands **Greeklish**: typing `mega`, `ant1` or `ert` matches `MEGA`, `ANT1`, `ΕΡΤ` and vice versa. Try both Greek and Latin spellings, and check **Search History** for past terms.
</details>

<details class="faq" markdown="1">
<summary markdown="span">How do I update, report a bug, or request a feature?</summary>

If you installed via the repository, updates arrive through Kodi automatically. For bugs and ideas use [GitHub Discussions](https://github.com/Twilight0/plugin.video.alivegr/discussions) — check existing threads first and include your Kodi version, platform, and steps to reproduce.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Does AliveGR host any videos?</summary>

No. AliveGR hosts nothing — it parses freely available public sources, acting strictly as a directory and search client. Availability depends on those third-party sources.
</details>

<details class="faq" markdown="1">
<summary markdown="span">How can I support development?</summary>

Via [Ko-fi](https://ko-fi.com/D1D11UQ0IO), [PayPal](https://www.paypal.me/AliveGR) or [Patreon](https://www.patreon.com/twilight0). See [Support](#support) below.
</details>

## Support

If you appreciate the time and continuous maintenance that goes into AliveGR, consider supporting future development:

* **Ko-fi**: [ko-fi.com/twilight0](https://ko-fi.com/D1D11UQ0IO)
* **PayPal**: [paypal.me/AliveGR](https://www.paypal.me/AliveGR)
* **Patreon**: [patreon.com/twilight0](https://www.patreon.com/twilight0)

* **Discussions, Feature Requests &amp; Bug Reporting**: [GitHub Discussions](https://github.com/Twilight0/plugin.video.alivegr/discussions)
* **Source**: [github.com/Twilight0/plugin.video.alivegr](https://github.com/Twilight0/plugin.video.alivegr)
* **Repository**: [github.com/Twilight0/repository.twilight0](https://github.com/Twilight0/repository.twilight0)

> **Disclaimer**: The author of AliveGR does not host, stream, or distribute any of the media content displayed within this software. All streams and on-demand links are parsed from publicly available domains on the internet. AliveGR acts strictly as a directory and search client.

</div>
</div>
