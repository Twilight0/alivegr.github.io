---
layout: post
lang: el
title: "subtitles.gr saga: 4.3.0 και το Τείχος του Android, ή Πώς Σταμάτησα να Στέλνω .so Αρχεία"
date: 2026-10-20 10:00:00 +0000
author: Twilight0
tags: [subtitles, technical, releases]
permalink: /el/news/subtitles-gr-4-3-0-android-saga/
---

Το Subtitles.gr 4.3.0 είναι διαθέσιμο. Αυτό είναι το τρίτο άρθρο της σειράς — μετά το [TLS impersonation](2026-10-09-subtitles-gr-tls-impersonation-and-curl-cffi-el.md) και [την παράδοση του captcha](2026-10-18-subtitles-gr-captcha-handoff-el.md) — και είναι αυτό όπου το Android δουλεύει επιτέλους. Ακολουθεί η διαδρομή, επεισόδιο προς επεισόδιο, γιατί το changelog από μόνο του δεν εξηγεί πόσες φορές έκανα λάθος πριν κάνω σωστό.

## Επεισόδιο 1: «Φορτώνει το curl_cffi;» (δεν φόρτωνε)

Ξεκίνησε με ένα log από Samsung A53: Kodi 21.2, Python 3.11, `script.module.curlcffi v0.16.3 installed` — και κάθε πάροχος που το χρειαζόταν να προσπερνάει με `needs script.module.curlcffi`. Εγκατεστημένο αλλά αδρανές. Η πρώτη μου διάγνωση ήταν το κενό στο `sys.path`: το Kodi βάζει στο path το σκέτο `lib/` ενώ το πακέτο κάθεται δύο επίπεδα πιο κάτω. Το διόρθωσα — και το επόμενο log είπε `No module named '_cffi_backend'`. Το πακέτο δεν είχε καθόλου cffi backend: τα upstream wheels το δηλώνουν ως pip dependency, και pip μέσα στο Kodi δεν τρέχει ποτέ. Στο desktop δούλευε μόνο από τύχη του περιβάλλοντος.

## Επεισόδιο 2: Ο builder αποκτά backend (και σπάει το CI τρεις φορές)

Έβαλα το `_cffi_backend` σε όλες τις πλατφόρμες στο [curl-cffi-builder](https://github.com/Twilight0/curl-cffi-builder): desktop από PyPI wheels ανά minor, Android/iOS/armv7l cross-compiled από το cffi sdist, συν libffi από πηγαίο κώδικα όπου ο στόχος δεν έχει. Στην πορεία ανέβασα σε curl_cffi 0.16.4b1 και impersonate v2.2.3. Το CI έσπασε, με τη σειρά: ένα `-bundle` που έλειπε στο iOS, ένα `<ffi.h>` που δεν υπάρχει πουθενά, μετά `pyconfig.h` που λείπει από τα CPython sources (παράγεται στο build time — τώρα κάνω compile κάθε minor με τα δικά του headers), μετά σφάλματα `LONG_BIT` και στους δύο 32-bit στόχους. Τέσσερα pushes, όλα πράσινα στο τέλος. Ήμουν περήφανος. Πήγαν όλα χαμένα.

## Επεισόδιο 3: noexec (το πείραμα της μίας γραμμής που το τελείωσε)

Με το backend επιτέλους μέσα, το log του κινητού έδωσε το πραγματικό σφάλμα: `dlopen failed ... not accessible for the namespace`. Αντέγραψα ένα binary στο emulated storage και προσπάθησα να το εκτελέσω: `Permission denied, rc=126`. Το Android μοντάρει το emulated storage `noexec`, και το linker namespace αρνείται οποιοδήποτε executable mapping από εκεί. **Καμία native βιβλιοθήκη μέσα σε addon του Kodi δεν μπορεί ποτέ να φορτώσει στο σύγχρονο Android.** Ολόκληρο το module των 92MB, ο builder matrix, η περιπέτεια του CI — αρχιτεκτονικά αδύνατα σε αυτή την πλατφόρμα. Όχι bug. Τοίχος.

## Επεισόδιο 4: ο Gujal00 είχε δίκιο

Εκεί γύρω [ο Gujal00 σημείωσε στο ResolveURL tracker](https://github.com/Gujal00/ResolveURL/issues/1509) ότι το Kodi 22 (Python 3.14 + OpenSSL 3.x) λύνει hosts με προστασία με σκέτο urllib — χωρίς modules. Η πύλη δεν ήταν ποτέ «ακριβώς Chrome»· ήταν «σύγχρονος client». Οπότε έχτισα ακριβώς αυτό, ρητά: ένα pure-Python transport με σειρά ciphers Chrome150, ALPN, χωρίς παλιά πρωτόκολλα, και το non-JS User-Agent που περνάει μόνο του τον Anubis. Επαλήθευσα το JA3 στο καλώδιο, μετά το κινητό — φρέσκο σε Kodi 22 RC1 — έτρεξε την αναζήτηση Subs4Series με μηδέν προκλήσεις. Το curl_cffi μένει πρώτη επιλογή όπου φορτώνει· το fallback καλύπτει όλα τα υπόλοιπα. Τίποτα native, τίποτα για εγκατάσταση, δουλεύει σε κάθε κουτί συμπεριλαμβανομένων αυτών που δεν μπορούν ποτέ να κάνουν dlopen.

## Επεισόδιο 5: το πραγματικό 4.3.0 (διορθώσεις και μικρές χάρες)

Με το transport τακτοποιημένο, σάρωσα τα υπόλοιπα:

- **Ξεκλείδωτα toggles παρόχων.** Οι έλεγχοι εγκατάστασης curl_cffi έφυγαν από Subs4Series, SubDL, Addic7ed και Translate — μένουν στον έλεγχο του χρήστη, με σημείωση ομάδας για το τι χρειάζεται κάθε στήσιμο. Το runtime αποφάσιζε ήδη ανά αίτημα· η οθόνη ρυθμίσεων το παραδέχεται επιτέλους.
- **Ελληνικά με ένα κλικ.** Νέα ενέργεια προσθέτει τα ελληνικά στη λίστα γλωσσών υποτίτλων του ίδιου του Kodi, κρατώντας τις υπάρχουσες. Σε φρέσκια εγκατάσταση αντικαθιστά τη διαδρομή Player → Γλώσσα → Προτιμώμενη γλώσσα υποτίτλων → διάλογος πολλαπλής επιλογής. Ένα κουμπί.
- **Φόρτωση τοπικού υπότιτλου.** Προαιρετική καταχώρηση πάνω από τα αποτελέσματα (μόνο όταν η αποθήκευση είναι ανοιχτή, το toggle είναι ανοιχτό, και υπάρχουν αποθηκευμένοι υπότιτλοι) ανοίγει τον file picker του Kodi για οποιοδήποτε `.srt/.sub/.ssa/.ass` και το παίζει από την κανονική διαδρομή.
- **Διόρθωση crash SubZTV σε non-ASCII URLs**, **διαγνωστικά προκλήσεων** (Ray ID + IP εξόδου στο log, σώμα για επιθεώρηση), **βάση Nexus** με τρέχοντα pins modules.

## Οι κανόνες της πλατφόρμας, όπως τους κατάλαβα πια

Για Android: Kodi 22 Piers, τελεία. Και το curl cffi είναι περιττό σε κάθε πλατφόρμα — πρώτη επιλογή όπου φορτώνει, αδιάφορο όπου καλύπτει το fallback. Παλαιότερα stacks μένουν στο 4.2.0.

Το Subtitles.gr 4.3.0 είναι στο αποθετήριο Twilight0 από τώρα.
