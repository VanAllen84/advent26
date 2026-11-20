# Adventskalender2026_AV_TAK
Adventskalender 2026

# Adventskalender 2026 – LIVE-Version

Persönlicher, erotischer Adventskalender für Anja, geschrieben und gebaut von Thilo.
Adresse: **https://kalender2026.tkagel.de** (GitHub Pages, statische Seite, kein Server, keine Datenbank).

> Diese Seite ist der echte Kalender. Alles, was hier geändert wird, sieht sie sofort.
> Ausprobiert und geändert wird zuerst in der TEST-Version (siehe README_TEST.md).

---

## 1. Worum es geht

Vom 1. bis 24. Dezember öffnet sich jeden Tag ein Türchen. Hinter jedem Türchen steckt:

1. **eine Geschichte in drei Stimmungen** – sie wählt, in welcher Stimmung sie die Geschichte lesen will,
2. **eine Aufgabe** (Karte), die am Ende der Geschichte genannt wird; sie zieht die passende Karte (den „Umschlag“) aus dem Beutel,
3. **eine Alternative** zur Aufgabe, falls ihr die eigentliche Aufgabe nicht passt.

Dazu gibt es analoge Teile: 24 gedruckte Faltkarten, den Beipackzettel (PDF), die Röllchen (Pappröhren Ø 5 cm × 10 cm) mit kleinen Gimmicks sowie die Gimmick-Zettel.
Ab dem 25. Dezember gibt es eine Auswertung ihrer Favoriten, abgeglichen mit Thilos eigenen Bewertungen.

## 2. Dateien in diesem Ordner (Repo)

| Datei / Ordner | Zweck |
|---|---|
| `index.html` | Die gesamte App (Aufbau, Design, Logik, Animationen). Eine einzige Datei. |
| `story-day1.js … story-day24.js` | Die Geschichten, je Tag eine Datei, je Datei drei Stimmungen. Werden erst beim Öffnen des Tages nachgeladen. |
| `data.js` | Die Aufgabentexte (Karten, Aufgabe a / Alternative b) in Base64 (`KARTEN_B64`). Wird bei Bedarf geladen. |
| `er.js` | **Thilos Bewertungen** (A/B/C je Aufgabe und Alternative). Wird erst ab dem 25.12. geladen (siehe 6.). |
| `bilder/` | Türchen-Bilder `karte-01.jpg … karte-24.jpg`, `finale.jpg`, `landing.jpg` und die verpixelten Vorschaubilder `pix-lock-XX.png`. |
| `erinnerung/*.ics` | Fertige Kalenderdateien mit 24 Terminen („Türchen 1 … 24“) in Uhrzeit-Varianten (17:00 bis 21:30). Sie holt sich die Seite über „Termine hinzufügen“. |
| `sw.js` | Service Worker (Zwischenspeicher, Offline-Fähigkeit). Siehe 7. |
| `manifest.json`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` | App-Eigenschaften für „Zum Home-Bildschirm hinzufügen“ (Name: „Dezember“). |

Nicht in LIVE enthalten: `er-editor.html` (das Werkzeug zum Eintragen von Thilos Bewertungen) – das gibt es nur in TEST.

## 3. Was die App kann

**Startseite**
- Titel, Begrüßung, Landing-Bild, Countdown („Noch X Tage …“, nur kurz vor dem 1.12.).
- Bereich „Bevor es losgeht“: Anleitung zum Hinzufügen zum Home-Bildschirm und die Funktion „Lass dich jeden Tag erinnern“ (Uhrzeit wählen, 24 Termine landen im Handy-Kalender).
- Kasten „Und so funktioniert das Ganze“ mit sieben Punkten (Stimmung, Geschichte, Umschlag, Bewerten, Notizen, Wiederfinden, Ab dem 25. Dezember).

**Türchen-Übersicht**
- Kacheln 1–24. Zustände: *gesperrt* (noch nicht dran), *heute*, *ausgelassen* (mit Hinweis „Noch ungeöffnet“), *geöffnet* (goldener Rand) und *frei* (nach dem 25.12.).
- Gesperrte Türchen zeigen ein verpixeltes Bild und wackeln beim Antippen mit Hinweis.
- Bei geöffneten Türchen steht unten eine **Kurzbeschreibung der Aufgabe** (ein bis drei Wörter, z. B. „Teaser tagsüber / Verwöhne nur ihn“) – damit sie wiederfindet, was sie noch bewerten möchte.

**Türchen öffnen (Animation)**
- Die Tür klappt auf, das verpixelte Bild **entpixelt** sich in mehreren Stufen, dann taucht man per Zoom in das Bild ein und landet in der Geschichte.
- Ist noch keine Stimmung gewählt, geht es zuerst in die Stimmungsauswahl.
- Als „Wasserzeichen“ bleibt das Bild des Tages dezent im Hintergrund.
- Beim Wechsel zur Geschichte wirbeln die Buchstaben („Buchstabenwirbel“).
- Bei „reduzierte Bewegung“ im Betriebssystem werden Animationen übersprungen.

**Stimmung & Geschichte**
- Drei Stimmungen pro Tag; die Wahl gilt für diesen Tag und kann nicht mehr geändert werden. Erst ab 25.12. dürfen die anderen Stimmungen gelesen werden.
- Am Ende der Geschichte: welcher Umschlag gezogen wird (Karte, Aufgabe + Alternative).

**Bewerten**
- Am nächsten Tag fragt das Türchen oben nach der Aufgabe vom Vortag. Aufgabe, Alternative oder beides, jeweils 👍 / 😐 / 👎.
- Auch direkt nach der Aufgabe bewertbar (Kasten am Ende der Türchenseite).
- Eine abgegebene Bewertung lässt sich noch bis zum Tag danach ändern; nachholen geht durch erneutes Öffnen des Türchens.

**Notizen**
- Pro Türchen ein Notizfeld („Meine Notiz zur Aktion (nur für dich)“, max. 600 Zeichen). Bleibt nur im Browser des Geräts.

**Ab dem 25. Dezember**
- Alle Türchen sind frei, die anderen Stimmungen lesbar.
- **Auswertung der Favoriten:** Ihre Bewertungen werden mit Thilos Bewertungen aus `er.js` abgeglichen. Es gibt Top-Favoriten (beide 👍) und Favoriten (einer 👍, einer 😐). Nur wenn Thilo ebenfalls bewertet hat, gibt es einen Abgleich; er sieht dafür keine Daten von ihr.
- **Rückblick** (Statistik: wie viele Türchen, Stimmungen, Bewertungen, Notizen).
- **Erinnerung speichern:** erzeugt Bilder (Rückblick, Favoriten) und eine Textdatei mit Bewertungen und Notizen.
- **Finale** (Überraschung nach dem letzten Türchen; Varianten A/B).

**Wolken-Knopf (Chef-Taste)**
- Der Knopf oben rechts versteckt die Seite sofort hinter einer Wetteransicht. Beim ersten Mal erscheint ein Hinweis („Kleiner Tipp“).

## 4. Zeitlogik in LIVE

- `testModus = false`: Die Entwickler-Leiste ist weg, Türchen öffnen sich nur an ihrem Tag (Türchen N ab dem N. Dezember; frühere Türchen bleiben offen).
- Es gibt in LIVE **keinen** `VORTEST_NOVEMBER`-Schalter: Das Datum ist das echte Datum.
- `alleFreigegeben()` wird am **25.12.2026** wahr (oder in späteren Jahren sofort).
- Maßgeblich ist die Uhr des Geräts. Stellt sie die Uhr um, ändern sich die Freischaltungen (der Kalender merkt sich aber, was geöffnet wurde).

## 5. Gespeichertes im Browser (localStorage)

Alles liegt **nur auf dem Gerät**, nichts geht an einen Server.

| Schlüssel | Inhalt |
|---|---|
| `adventGeoeffnet26` | welche Türchen geöffnet wurden |
| `adventWahl26` | gewählte Stimmung je Tag |
| `adventBewertung26`, `adventBewDatum26` | ihre Bewertungen und das Datum, wann bewertet wurde |
| `adventNotiz26` | ihre Notizen |
| `adventLese26` | welche Geschichten gelesen wurden |
| `adventGruss26` | Begrüßung gesehen |
| `adventBossHint26` | Wolken-Hinweis bereits gelesen |
| `adventFinaleAn26` | Finale gesehen |
| `adventSpaeter26` | Bewertung auf später verschoben |

Das **Zurücksetzen** geschieht mit `https://kalender2026.tkagel.de/?reset=1`. Es löscht Geöffnet, Wahl, Bewertungen, Datum, Später, Notizen und Gelesen und lädt die Seite danach ohne den Zusatz neu. Nicht gelöscht werden Begrüßung, Wolken-Hinweis und Finale-Marker.
**In LIVE nicht auf ihrem Handy ausführen!** Damit sind alle Wahlen und Bewertungen weg. Wenn sie Browserdaten löscht oder den Browser wechselt, ist ebenfalls alles weg.

## 6. Thilos Bewertungen (`er.js`)

- Pro Türchen zwei Buchstaben: 1. Aufgabe, 2. Alternative. `"A"` = 👍, `"B"` = 😐, `"C"` = 👎, `""` = nicht gemacht.
- `er.js` wird **erst ab dem 25.12.** geladen. Der Inhalt ist daher vorher zwar im Repo sichtbar, aber nicht in der App.
- Bevor es ernst wird, in LIVE prüfen, dass `er.js` die **echten** Bewertungen enthält und nicht den Platzhalter.
- Befüllt wird `er.js` am einfachsten mit `er-editor.html` aus der TEST-Version; den fertigen Text kopieren und als `er.js` committen.
- Fehler in der Datei (fehlendes Komma, Anführungszeichen) führen dazu, dass der Abgleich fehlt. Die Seite stürzt aber nicht ab.

## 7. Service Worker & Updates (`sw.js`)

- Seiten und Geschichten: erst Netzwerk, bei Fehler Zwischenspeicher. Bilder (`/bilder/`): erst Zwischenspeicher.
- **Nach jeder Änderung an `index.html` (oder anderen Dateien) die `VERSION` in `sw.js` ändern**, z. B. `const VERSION = "v1795178612";`. Sonst kann ihr Handy alte Inhalte behalten.
- Wenn nach einem Upload nichts Neues zu sehen ist: Seite komplett schließen und neu öffnen; als Notlösung die App vom Home-Bildschirm entfernen und neu hinzufügen.

## 8. Update-Vorgang in LIVE (Checkliste)

1. Änderung in TEST bauen und prüfen (siehe README_TEST.md).
2. Dieselben Änderungen in LIVE übernehmen. **Achtung:** Die beiden `index.html` unterscheiden sich im Wesentlichen nur durch den `VORTEST_NOVEMBER`-Block und die Test-Diagnose; nie einfach die TEST-Datei kopieren, ohne den Unterschied zu prüfen.
3. `VERSION` in `sw.js` erhöhen.
4. Hochladen/committen. GitHub Pages braucht meist ein bis zwei Minuten.
5. Auf dem eigenen Handy `https://kalender2026.tkagel.de` öffnen und prüfen (nicht `?reset=1`, wenn es ihr Handy wäre).

## 9. Wichtige Hinweise

- Die Seite enthält `noindex, nofollow` und ist nicht verlinkt; geheim ist sie dadurch aber nicht. Wer die Adresse kennt, kann sie öffnen.
- Alle Texte sind deutsch. Fachwörter: „Umschlag“ = Ziehen aus dem Beutel, „Karte“ = die Aufgabe.
- Zur Sicherheit existiert ein Backup als `advent26-LIVE_komplett.zip` (wird auf Wunsch aktualisiert).
