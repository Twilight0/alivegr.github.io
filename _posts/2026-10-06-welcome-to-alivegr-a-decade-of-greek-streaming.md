---
layout: post
title: "Welcome to AliveGR: Ten Years of Greek Streaming, Stubbornness, and Sleepless Nights"
date: 2026-10-06 10:00:00 +0000
author: Twilight0
---

Welcome. Sit down, grab a coffee — a proper Greek one, not that dishwater they serve tourists — because this story is ten years long and I am going to tell it the way it actually happened.

**AliveGR** (stylized exactly like that, and yes, people still get it wrong) is a Kodi addon for streaming content mostly in Greek: live TV, movies, series, sports, music, radio, news, kids content, documentaries. It hosts nothing. It is a search engine over freely available public sources. That one sentence has taken me a decade to be able to write with a straight face. Let me explain.

## 2016: no antenna, no clue, no sense

The year is 2016. I do not own a DVB-T antenna. Greek digital terrestrial television is right there, in the air, free, and I cannot watch any of it because I never got around to buying a ten-euro piece of metal. There is an existing addon — Hellenic TV — and it is broken in the ways that mattered to me. The natural response of a sane person: file a bug report, wait, maybe contribute a patch.

I was not sane. I decided to build the whole thing from scratch instead.

Why? Because fixing someone else's architecture means inheriting someone else's assumptions, and I had Opinions (capital O, as always). I wanted one addon for *everything* Greek, not a live-TV shim plus five other addons duct-taped together. One menu. One search. One experience your father-in-law can use without calling you. And to do that, I first had to teach myself to code — properly, not tutorial-level, but "parse hostile HTML at 2 AM" level. Endless sleepless nights. Python tracebacks burned into my retinas. My commit history from that era reads like a sleep-deprivation diary, and frankly it was.

The irony, which I savour daily: I eventually got an antenna. It has since broken. Ten years later I am back to needing my own addon. The circle of life, Greek streaming edition.

## The TVAddons years: ag, offshoregit, co

If you were in the Kodi scene in 2017, you remember June of that year the way normal people remember where they were during earthquakes. TVAddons.ag — the Fusion repository, some 1,500 addons, the beating heart of third-party Kodi — got hit with lawsuits and shut down overnight. Domains seized, developers lawyering up, users staring at dead update URLs.

AliveGR lived through all of it. The addon rode the migration from **TVAddons.ag** to the **offshoregit** stopgap and eventually to **TVAddons.co**, the resurrection domain. Each move meant new repository zips, new update paths, confused users asking why their addon stopped updating, and me explaining DNS and GitHub hosting to people who just wanted to watch the news. Those were the years AliveGR went from a personal project to infrastructure — something strangers depended on, which is both flattering and terrifying.

The commit counts tell the story: 66 commits in 2017, 59 in 2018. That is not a hobby. That is a second job with no pay and angry customers.

## 2018: banned from the Kodi forums (the funny part — and the true story)

In 2018 I got banned from the official Kodi forums. Here is the true story, briefly — judge for yourself.

My friend bugatsinho, crypto-obsessed then and now (I am not — I consider it gambling), had built Monero-based "shortened" links: proof-of-work openers mining a miniscule amount via the visitor's CPU. As a favour, I routed my Kodi program addon through them — it whitelisted users' IPs for video playback, and the authorization page passed briefly through those links first. I was a naive hobbyist, did not think it through. That was wrong, and I own it: the links were opt-*out* rather than opt-in, exactly backwards, as users rightly pointed out after my apology. Worse, the addon was half-broken by design — the browser-based auth flow simply died on Android boxes, LibreELEC, Fire sticks — so many users got the miner gate with no working feature behind it. Useless *and* wrong, entirely my design.

Then came the farce: someone blogged about it, Reddit picked it up, and Team Kodi stepped in and made me the scapegoat — instant zero-tolerance theatre, the same treatment they had given plenty of developers before me. No discussion of opt-in versus opt-out, no remediation path, just the ban. A proportionate response (forced removal, fix to opt-in, probation) would have repaired the actual harm; the ban merely performed something. It punished the person instead of fixing the problem — which is precisely why it was disproportionate.

So I protested the only way a developer can: I pushed a **blank version** of the addon. Version history shows it plainly — June 24th, 2018, commit message *"Blank addon push"*: every file gutted, code deleted, an empty shell where AliveGR used to be. The message to the forums, and to the users begging them to unban me: *fine, no addon then — see how you like that.* Users, bless them, actually petitioned for my recall. The ban stood, the addon came back, and the blank commit remains in the git history as a monument to spite. I am weirdly proud of it.

## The versions: why each one exists

- **1.x (2017–2019):** the wild years. Rapid iteration, sometimes multiple releases a day — September 2017 alone has a dozen version bumps. Every Greek site changed its markup weekly, every fix broke two other things. This is the era users remember fondly and I remember as trauma.
- **Blank (June 2018):** the protest push described above. Not a version, a statement.
- **2.x (2020):** the great rewrite. After the 1.x architecture collapsed under its own weight, January 2020 saw an insane sprint — alpha1 through alpha13 in *ten days* — culminating in 2.0.0 final on January 30th. A proper framework-based addon instead of a pile of scrapers. This is the version that survived for years.
- **2023–2026: the hiatus.** Three years of near-silence — four commits in all of 2023, real life intervening the way it does. The addon kept breathing on life support while I was elsewhere. Every returning developer knows this guilt: the issue tracker filling up while you are busy being a person.
- **2026: the return, twice refactored.** And then AI-assisted development happened, and I mean *happened* — productivity up easily tenfold. The boring 80% (boilerplate, test matrices, rebase archaeology, markup adaptations) gets done by the machine; I spend my time on judgment calls. 2026 saw not one but **two major refactorings**, marching through 3.0.0 alphas all spring to the 3.0.0 beta1 in October. The addon is cleaner now than it has ever been, and most of the credit goes to a workflow that did not exist three years ago.

## Why this site exists

alivegr.app is the addon's long-overdue home: documentation, news, and a place that is *mine* — no forum moderators, no repository politics, no blank pushes required. The addon lives at [github.com/Twilight0/plugin.video.alivegr](https://github.com/Twilight0/plugin.video.alivegr), installs via the [repository.twilight0](https://github.com/Twilight0/repository.twilight0) zip, and the front page covers what it does.

Ten years, hundreds of commits, one forum ban, one spite-push, one three-year nap, and two AI-powered refactorings. The antenna is broken again. The addon works. Some things never change — and some things finally do.

Have fun.
