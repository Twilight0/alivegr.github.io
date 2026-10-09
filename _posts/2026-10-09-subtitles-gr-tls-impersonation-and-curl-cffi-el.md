---
layout: post
lang: el
title: "Subtitles.gr στα ενδότερα: Νεκροί πάροχοι, TLS impersonation και curl_cffi"
date: 2026-10-09 19:00:00 +0000
author: Twilight0
permalink: /el/news/subtitles-gr-tls-impersonation-curl-cffi/
---

Μερικά επιπλέον, πιο τεχνικά λόγια για το Subtitles.gr v4.0.0 — συγκεκριμένα για το ποιοι πάροχοι επέζησαν, γιατί δύο από αυτούς είναι απενεργοποιημένοι εξ ορισμού, και τι σχέση έχει το `curl_cffi` με όλα αυτά.

## Τι επέζησε, τι όχι

Ωμά: οι αρχικοί πάροχοι έχουν χαθεί. Μόνο το όνομα έμεινε (και η γλώσσα).

* **Δουλεύουν out of the box:** Subs4Free, GreekSubs.net, YIFI, TVsubtitles.net, Moviesubtitles.org.
* **Αποσύρθηκαν:** Vipsubs.gr, Xsubs.tv, Podnapisi.net — νεκροί ιστότοποι, αφαιρέθηκαν.
* **Απενεργοποιημένα εξ ορισμού:** το ίδιο το domain `subtitles.gr` (δεν φορτώνει, οι scrapers του δεν ενημερώθηκαν), plus τα SubDL και Subs4Series — για έναν πιο ενδιαφέροντα λόγο, παρακάτω.

## Γιατί τα SubDL και Subs4Series χρειάζονται «hack»

Οι διακομιστές αυτών των δύο ιστότοπων απαιτούν **TLS fingerprinting με προχωρημένη συμπεριφορά HTTP**: επιθεωρούν το TLS ClientHello του πελάτη (cipher suites, extensions, σειρά — την υπογραφή JA3) και απορρίπτουν οτιδήποτε δεν μοιάζει με πραγματικό browser. Το σκέτο `urllib` — ή οτιδήποτε χτισμένο πάνω στο module `ssl` της Python με προεπιλεγμένες ρυθμίσεις — αποτυγχάνει στον έλεγχο handshake πριν καν ανταλλαγεί HTTP.

Η λύση έχει όνομα: [curl_cffi](https://github.com/yifeikong/curl_cffi) — Python bindings για ένα patched curl (curl-impersonate) που αναπαράγει πραγματικά δακτυλικά αποτυπώματα browser τόσο στο επίπεδο TLS όσο και στο HTTP/2. Με ενεργό το impersonation, οι διακομιστές βλέπουν «Chrome» αντί για «ένα Python script» και σερβίρουν κανονικά τις λήψεις υποτίτλων.

## Το πρόβλημα του build: native κώδικας στο Kodi

Το `curl_cffi` δεν είναι καθαρή Python — τυλίγει μια μεταγλωττισμένη native βιβλιοθήκη. Οι στόχοι του Kodi δεν έχουν compiler, και το αποθετήριο Twilight0 εξυπηρετεί τα πάντα, από Linux desktop και LibreELEC μέχρι Android (FireTV, Shield, κινητά) με όλες τις ιδιοτροπίες του: πολλαπλά ABI (`arm64-v8a`, `armeabi-v7a`, `x86_64`), NDK toolchains, επίπεδα API.

Για να δουλέψει αυτό έπρεπε να φτιάξω **builder scripts και προμεταγλωττισμένα Python wheels** — «συνταγές» που μεταγλωττίζουν τον native κώδικα ανά πλατφόρμα, ώστε κάθε συσκευή να κατεβάζει το ταιριαστό δυαδικό αντί να χτίζει από τον πηγαίο κώδικα. Το Android, με τις πολλές ιδιοτροπίες του, ήταν το δύσκολο κομμάτι.

## Πώς τα ενεργοποιείτε

Τα SubDL και Subs4Series μένουν σκόπιμα opt-in — οι περισσότεροι χρήστες δεν τα χρειάζονται ποτέ, και η native εξάρτηση είναι βαριά. Για να τα ανάψετε:

1. Ανοίξτε τις **Ρυθμίσεις του Subtitles.gr → Ενέργειες → Install curl_cffi** και αφήστε το ταιριαστό wheel να εγκατασταθεί.
2. Γυρίστε τα SubDL και Subs4Series σε κατάσταση **ενεργοποιημένα** στη λίστα παρόχων.

Όλα τα υπόλοιπα — Subs4Free, GreekSubs, YIFI, TVsubtitles.net, Moviesubtitles.org — δεν χρειάζονται τίποτα και δουλεύουν αμέσως μετά την εγκατάσταση του προσθέτου από το Αποθετήριο Twilight0.
