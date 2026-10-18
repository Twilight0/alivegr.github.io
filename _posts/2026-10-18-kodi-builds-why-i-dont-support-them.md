---
layout: post
lang: en
title: "Kodi Builds: Why I Don't Support Them, and Why Trust Beats Convenience"
date: 2026-10-18 12:00:00 +0000
author: Twilight0
permalink: /en/news/kodi-builds-why-i-dont-support-them/
---

I do not support the use of builds. Period. Full stop. No asterisk, no "but if you really want to," no diplomatic hedge. If you came here for a balanced take, this is not that post.

Let me explain why, technically, and with the appropriate amount of irritation.

## The control problem

A build is not an add-on. It is an entire pre-configured Kodi installation — skin, settings, fonts, playlists, sources, and dozens of add-ons — packaged by someone else and installed as a single blob.

I have no control over what is inside that blob. I cannot audit it. I cannot see which version of which dependency it ships. And everything inside it runs in the same environment as my add-ons.

That last part is the crux. Kodi add-ons are not sandboxed like Flatpaks. They run in a shared Python runtime, and they depend on shared `script.module.*` packages. When an add-on needs `script.module.resolveurl`, it imports whatever copy the system hands it. If a build ships its own modified version of that module, every add-on that depends on it gets the modified behaviour — silently, and without your knowledge.

This is not theoretical paranoia. This is how Python imports work.

## The AI wildcard

Now add AI to the mix, which is exactly what has happened over the last year or two.

Build maintainers who could not write a `for` loop six months ago can now ask a model to "optimize" the code inside their build. The model does not know it is editing someone else's add-on. It does not know what the author's intent was. It just applies patterns — the maintainer's patterns, or the model's own defaults — to code it barely understands.

A concrete example: automatic texture cache cleanup for items older than a given age. That is not inherently a bad idea. It might even help on a low-storage device. But it is not something Kodi does by default. It is a behaviour someone added, with AI assistance, to code they did not write, affecting an environment they do not fully comprehend.

Multiply that by the fifty-odd "optimizations" a typical build bakes in, and you start to see the problem. My add-ons now run inside someone else's opinions about how Kodi should behave.

## The irony: Kodi already does this

Here is the part that actually gets me.

The Kodi developers — the people who wrote the platform — built it so that this kind of maintenance happens automatically. Cache management, library updates, cleanup, database maintenance: handled by Kodi itself, out of the box, no intervention required.

That is the entire point of a platform. It manages itself.

And yet the build scene's answer to everything is a wizard.

## The wizards

Oh, the wizards.

A "wizard" in this context is a badly written add-on that carries legacy code from the Jarvis era — that is Kodi 16, released in 2016. Ten years of accumulated cruft, calling patterns that were deprecated before some of these builds had users, wrapping functionality Kodi already provides natively.

They clean things that do not need cleaning. They "fix" things that are not broken. They run on first boot, and on every boot after that, and they quietly change the state of the system underneath your add-ons.

Wizards exist to make a build feel like a product. What they actually do is add another moving part to a machine that was working fine without it.

## Most build maintainers are not programmers

I say this without malice, but it needs to be said plainly, because it is the root of the trust problem.

Most people who assemble builds are not developers. They are enthusiasts, packagers, hobbyists who are very good at following installation guides and very willing to spend their evenings wrangling add-ons into a coherent-looking package. That is a real skill. But it is not the same skill as reading a Python traceback, or understanding why importing a modified `script.module` shadows another add-on's dependency, or knowing what a race condition does to a shared library index.

Combine limited programming knowledge with AI-generated code edits, and you get builds that work flawlessly on the maintainer's device and mysteriously on nobody else's.

## Trust is now the whole game

Which brings me to the conclusion.

The trust you extend to a build maintainer has never mattered more, and has never been harder to justify. You are not just trusting them to pick good add-ons. You are trusting them not to break the add-ons you depend on, not to ship modified dependencies, not to let a language model rewrite code no one will review, and not to sprinkle wizards over a platform that maintains itself.

Most builds cannot honestly pass that test. Not because everyone is malicious — almost nobody is — but because nobody can audit a blob of fifty add-ons plus a decade-old wizard plus AI edits, and claim with a straight face that they know what it does.

## Pluralism is exhausting

There is a second problem, subtler than trust but just as damaging: pluralism for its own sake.

The build scene's selling point is variety. Thousands of add-ons, endless categories, a build for every mood and every provider and every country. It sounds generous. In practice, it tires everyone out and adds one more point of failure for every add-on you install.

You do not need four hundred add-ons. You do not need twelve sources for the same channel. You need one good add-on for live TV — something like AliveGR — and one good add-on for movies and series. Two. That is the entire list.

Everything beyond that is not capability. It is duplication dressed up as choice, and every duplicated dependency is another opportunity for something to break.

## What to do instead

Keep it small. Keep it honest. Keep it yours.

- Install add-ons directly, from their own repositories — including mine. Know what you are running and where it came from.
- Keep a short list: a live-TV add-on, a movies/series add-on, and the shared modules they actually need. Nothing else.
- Let Kodi do its own maintenance. It was built to.
- No wizards. If something needs a wizard to keep working, the answer is not a wizard — it is a better add-on.
- If you must use a build, understand that you are trading trust for convenience, and that the code you are running was assembled by someone who, statistically, cannot tell you what it does.

I maintain add-ons that people rely on. I am responsible for what happens when those add-ons run. I cannot be responsible for what happens when they run inside an environment nobody audited, wrapped in decade-old wizard code, edited by a model that has never seen the source.

So: I do not support builds. Period.

If that costs me users, so be it. The ones who stay are the ones who understand.
