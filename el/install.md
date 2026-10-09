---
layout: default
lang: el
title: Εγκατάσταση & FAQ
description: Πώς να εγκαταστήσετε το AliveGR στο Kodi μέσω του αποθετηρίου Twilight0 ή απευθείας zip, προτεινόμενες ρυθμίσεις, συμβατότητα και συχνές ερωτήσεις.
permalink: /el/install/
---

<div class="post">
<div class="post-content" markdown="1">

## Εγκατάσταση &amp; FAQ

Όλα σε ένα μέρος: εγκατάσταση (από το [README του plugin.video.alivegr](https://github.com/Twilight0/plugin.video.alivegr/blob/master/README.md)), προτεινόμενες ρυθμίσεις, συμβατότητα και απαντήσεις σε συχνές ερωτήσεις.

<div class="install-toc" markdown="1">
**Σε αυτή τη σελίδα:** [Εγκατάσταση](#εγκατάσταση) · [Προτεινόμενες ρυθμίσεις](#προτεινόμενες-ρυθμίσεις) · [Συμβατότητα](#συμβατότητα) · [FAQ](#faq) · [Υποστήριξη](#υποστήριξη)
</div>

## Εγκατάσταση

### Μέθοδος 1: Μέσω του Αποθετηρίου Twilight0 (Προτείνεται)

Η εγκατάσταση μέσω του αποθετηρίου εξασφαλίζει ότι όλες οι εξαρτήσεις, οι επιλυτές και οι μελλοντικές ενημερώσεις εγκαθίστανται αυτόματα:

1. Στο Kodi, μεταβείτε στις **Ρυθμίσεις** (εικονίδιο γραναζιού) → **Διαχείριση αρχείων** → **Προσθήκη πηγής**.
2. Επιλέξτε `<Καμία>` και εισάγετε την ακόλουθη διεύθυνση URL:
   ```text
   https://twilight0.github.io/repository.twilight0/
   ```
3. Εισάγετε ένα όνομα για την πηγή (π.χ. `Twilight0 Repo`) και πατήστε **OK**.
4. Επιστρέψτε στην αρχική οθόνη του Kodi, πατήστε **Πρόσθετα** → **Περιηγητής προσθέτων** (εικονίδιο ανοιχτού κουτιού πάνω αριστερά).
5. Επιλέξτε **Εγκατάσταση από αρχείο zip** (ενεργοποιήστε τις *Άγνωστες πηγές* αν σας ζητηθεί).
6. Επιλέξτε `Twilight0 Repo` και πατήστε `repository.twilight0-2.0.zip`.
7. Μόλις εγκατασταθεί το αποθετήριο, επιλέξτε **Εγκατάσταση από αποθετήριο** → **Twilight0 Repository** → **Πρόσθετα βίντεο** → **AliveGR** → **Εγκατάσταση**.

### Μέθοδος 2: Απευθείας λήψη Zip

Μπορείτε επίσης να κατεβάσετε το αρχείο ZIP του αποθετηρίου απευθείας:

* Αρχείο ZIP αποθετηρίου: [repository.twilight0.zip](https://raw.githubusercontent.com/Twilight0/repository.twilight0/gh-pages/repository.twilight0.zip)

Μετά τη λήψη, στο Kodi μεταβείτε στα **Πρόσθετα** → **Περιηγητής προσθέτων** → **Εγκατάσταση από αρχείο zip**, επιλέξτε το αρχείο και συνεχίστε από το βήμα 7 παραπάνω.

## Προτεινόμενες ρυθμίσεις

Για την καλύτερη εμπειρία προβολής:

1. Βεβαιωθείτε ότι το **InputStream Adaptive** είναι ενεργοποιημένο:
   * **Ρυθμίσεις** Kodi → **Πρόσθετα** → **Τα πρόσθετά μου** → **VideoPlayer InputStream** → **InputStream Adaptive** → **Ενεργοποίηση**.
2. Στις ρυθμίσεις του AliveGR:
   * **Ροές**: Αφήστε τον *Επιλογέα ροής ζωντανής τηλεόρασης* στο `Adaptive` ή `Best` ανάλογα με τη σύνδεσή σας.
   * **Εμφάνιση**: Επιλέξτε το προτιμώμενο θέμα εικονιδίων (προτείνεται το `Gemini`).
   * **Φάκελοι**: Απενεργοποιήστε όσες κατηγορίες δεν χρησιμοποιείτε για καθαρότερο κεντρικό μενού.

## Συμβατότητα

* **Δοκιμασμένες εκδόσεις Kodi:** 20 (Nexus), 21 (Omega), 22 (Piers — υπό εξέλιξη).
* **Υποστηριζόμενες πλατφόρμες:** Linux (Garuda / Arch, Debian / Ubuntu, LibreELEC, CoreELEC), Android / Android TV / Google TV (FireTV, Nvidia Shield, smart TV, κινητά), Windows (x86_64), macOS / iOS / tvOS.
* **Βασικές απαιτήσεις:** [inputstream.adaptive](https://github.com/xbmc/inputstream.adaptive) (ενσωματωμένο δυαδικό πρόσθετο του Kodi, απαραίτητο για HLS/DASH και αναπαραγωγή DRM), plus εξαρτήσεις που εγκαθίστανται αυτόματα μέσω του αποθετηρίου Twilight0 (tulip, ResolveURL + PluginsGR, unicache, netclient, scrapetube, artwork AliveGR).

## FAQ

<details class="faq" markdown="1">
<summary markdown="span">Ποια μέθοδο εγκατάστασης να χρησιμοποιήσω;</summary>

Χρησιμοποιήστε τη **Μέθοδο 1 (αποθετήριο)**. Φέρνει αυτόματα όλες τις εξαρτήσεις και κρατά το AliveGR ενημερωμένο. Το απευθείας zip χρειάζεται μόνο αν δεν μπορείτε να προσθέσετε πηγή αρχείων στο Kodi.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Το Kodi ρωτά για «Άγνωστες πηγές». Είναι φυσιολογικό;</summary>

Ναι. Το Kodi το εμφανίζει όταν εγκαθιστάτε από αρχείο zip. Ενεργοποιήστε το όταν σας ζητηθεί, εγκαταστήστε το zip του αποθετηρίου και μετά μπορείτε να το αφήσετε ενεργό ή να το απενεργοποιήσετε ξανά.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Ποιες εκδόσεις Kodi και συσκευές υποστηρίζονται;</summary>

Τα Kodi 20 και 21 είναι δοκιμασμένα· η υποστήριξη Kodi 22 είναι υπό εξέλιξη. Υποστηρίζονται Linux, Android / Android TV / Google TV, Windows, macOS / iOS / tvOS — συμπεριλαμβανομένων LibreELEC / CoreELEC, FireTV / Shield και κινητών.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Χρειάζομαι το InputStream Adaptive / Widevine;</summary>

Ναι, βεβαιωθείτε ότι το **InputStream Adaptive** είναι ενεργοποιημένο (δείτε παραπάνω). Οι ροές με DRM χρειάζονται Widevine, το οποίο το Kodi φέρνει μέσω του InputStream Adaptive στην πρώτη χρήση. Χωρίς αυτό, τα HLS/DASH και τα κρυπτογραφημένα κανάλια θα αποτυγχάνουν.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Ένα κανάλι δεν παίζει, κολλάει ή λέει ότι είναι γεωγραφικά περιορισμένο. Τι κάνω;</summary>

Το AliveGR δοκιμάζει αυτόματα εναλλακτικές ροές. Αν μία αποτύχει, δοκιμάστε την επιλογή **«Επιλογή ροής»** από το μενού περιβάλλοντος του καναλιού για άλλη πηγή, ή αλλάξτε τον *Επιλογέα ροής* μεταξύ `Adaptive` και `Best` στις ρυθμίσεις. Ορισμένες πηγές είναι γεωγραφικά κλειδωμένες εκτός Ελλάδας/Κύπρου — αυτός είναι περιορισμός της πηγής, όχι σφάλμα.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Adaptive ή Best — τι να διαλέξω;</summary>

Το `Adaptive` προσαρμόζει την ποιότητα στη σύνδεσή σας (καλύτερο για αργές ή ασταθείς συνδέσεις). Το `Best` δοκιμάζει πάντα την υψηλότερη ποιότητα. Ξεκινήστε με `Adaptive` εκτός αν έχετε σίγουρα άφθονο εύρος ζώνης.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Η αναζήτηση δεν βρίσκει το κανάλι μου. Κάποιο κόλπο;</summary>

Η αναζήτηση καλύπτει ζωντανή τηλεόραση, ταινίες, σειρές, εκπομπές, θέατρο και κινούμενα σχέδια, και η αναζήτηση ζωντανής τηλεόρασης καταλαβαίνει **Greeklish**: πληκτρολογώντας `mega`, `ant1` ή `ert` βρίσκετε `MEGA`, `ANT1`, `ΕΡΤ` και αντίστροφα. Δοκιμάστε και ελληνική και λατινική γραφή, και δείτε το **Ιστορικό αναζήτησης**.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Πώς ενημερώνω, αναφέρω σφάλμα ή ζητάω λειτουργία;</summary>

Αν εγκαταστήσατε μέσω αποθετηρίου, οι ενημερώσεις έρχονται αυτόματα από το Kodi. Για σφάλματα και ιδέες χρησιμοποιήστε τα [GitHub Discussions](https://github.com/Twilight0/plugin.video.alivegr/discussions) — ελέγξτε πρώτα τα υπάρχοντα θέματα και συμπεριλάβετε έκδοση Kodi, πλατφόρμα και βήματα αναπαραγωγής.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Το AliveGR φιλοξενεί βίντεο;</summary>

Όχι. Το AliveGR δεν φιλοξενεί τίποτα — αναλύει ελεύθερα διαθέσιμες δημόσιες πηγές, λειτουργώντας αυστηρά ως κατάλογος και πελάτης αναζήτησης. Η διαθεσιμότητα εξαρτάται από αυτές τις τρίτες πηγές.
</details>

<details class="faq" markdown="1">
<summary markdown="span">Πώς μπορώ να στηρίξω την ανάπτυξη;</summary>

Μέσω [Ko-fi](https://ko-fi.com/D1D11UQ0IO), [PayPal](https://www.paypal.me/AliveGR) ή [Patreon](https://www.patreon.com/twilight0). Δείτε την [Υποστήριξη](#υποστήριξη) παρακάτω.
</details>

## Υποστήριξη

Αν εκτιμάτε τον χρόνο και τη συνεχή συντήρηση του AliveGR, στηρίξτε τη μελλοντική ανάπτυξη:

* **Ko-fi**: [ko-fi.com/twilight0](https://ko-fi.com/D1D11UQ0IO)
* **PayPal**: [paypal.me/AliveGR](https://www.paypal.me/AliveGR)
* **Patreon**: [patreon.com/twilight0](https://www.patreon.com/twilight0)

* **Συζητήσεις, Αιτήματα λειτουργιών &amp; Αναφορές σφαλμάτων**: [GitHub Discussions](https://github.com/Twilight0/plugin.video.alivegr/discussions)
* **Πηγαίος κώδικας**: [github.com/Twilight0/plugin.video.alivegr](https://github.com/Twilight0/plugin.video.alivegr)
* **Αποθετήριο**: [github.com/Twilight0/repository.twilight0](https://github.com/Twilight0/repository.twilight0)

> **Αποποίηση ευθύνης**: Ο δημιουργός του AliveGR δεν φιλοξενεί, δεν μεταδίδει ούτε διανέμει κανένα από τα μέσα που εμφανίζονται σε αυτό το λογισμικό. Όλες οι ροές και οι σύνδεσμοι αναλύονται από δημόσια διαθέσιμους ιστότοπους στο διαδίκτυο. Το AliveGR λειτουργεί αυστηρά ως κατάλογος και πελάτης αναζήτησης.

</div>
</div>
