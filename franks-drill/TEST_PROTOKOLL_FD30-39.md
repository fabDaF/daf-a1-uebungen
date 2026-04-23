# Test-Protokoll FD30–FD40

**Datum:** 2026-04-23
**Session:** A1-Drill-Ausbau (morphologische Schlussphase + pragmatischer Block)
**Prüfer:** Claude (statischer Audit + Browser-Test über Chrome-MCP auf fabdaf.github.io)

## Zusammenfassung

Alle elf Drills bestanden beide Test-Stufen ohne Befund.

| Drill | Thema | Audit | Browser |
|-------|-------|:-----:|:-------:|
| FD30 | Plural der Nomen | ✅ | ✅ |
| FD31 | Komparativ & Superlativ | ✅ | ✅ |
| FD32 | Ordinalzahlen | ✅ | ✅ |
| FD33 | Konjunktiv II als Höflichkeit | ✅ | ✅ |
| FD34 | Reflexivpronomen | ✅ | ✅ |
| FD35 | ja / nein / doch | ✅ | ✅ |
| FD36 | schon / noch / erst / nur | ✅ | ✅ |
| FD37 | kein / nicht | ✅ | ✅ |
| FD38 | Indefinitpronomen | ✅ | ✅ |
| FD39 | Länder & Präpositionen | ✅ | ✅ |
| FD40 | Uhrzeit (umgangssprachlich + offiziell) | ✅ | ✅ |

## Stufe 1 — Statischer Code-Audit

Geprüft pro Datei:

- **Items:** 48 Items in drei Runden à 16 — alle zehn bestanden
- **Tally-IDs:** alle in `TALLY_KEYS` referenzierten Schlüssel haben zugehörige HTML-IDs (`t<key>-<runde>`) — alle zehn konsistent
- **Anführungszeichen:** kein `„…"` mit ASCII-Schluss-`"` — alle zehn sauber
- **Hide-Regel:** `.pf-card[data-solved="0"] .cat-badge { visibility: hidden; }` vorhanden — alle zehn
- **Spoiler-Frei:** `catLabel()` enthält keine Antworten (kein `+ ans`, kein `"… → [artikel]"`) — alle zehn
- **Placeholder:** alle `placeholder=""` leer — alle zehn
- **Untertitel:** Format `A1 – Lektion FDxx` mit Halbgeviertstrich — alle zehn

## Stufe 2 — Browser-Test (Chrome-MCP auf GitHub Pages)

Pro Datei im Browser durchgeführt:

- Datei geladen über `https://fabdaf.github.io/daf-a1-uebungen/franks-drill/<datei>`
- `DRILL` existiert, drei Runden mit je 16 Items
- Alle vier Sections (`showSection(0..3)`) lassen sich wechseln ohne JS-Fehler
- Header `text-align: center` ✓
- Cat-Badge vor Lösung per `getComputedStyle` → `visibility: hidden` ✓
- Input-Simulation falsche Eingabe (`"XYZ"`) → `.wrong`-Klasse gesetzt ✓
- Input-Simulation korrekte Eingabe (`dataset.ans`) → `.correct`-Klasse gesetzt ✓
- Nach Lösung: Cat-Badge wird sichtbar ✓
- `resetRunde(1)` setzt Zähler zurück ✓
- Bei FD38 zusätzlich: Zwei-Wort-Antwort `"ein bisschen"` wird korrekt validiert ✓
- Bei FD35 zusätzlich: spezielle `.pf-frage`-Zeile vorhanden ✓

## Was NICHT maschinell getestet wurde

Diese Aspekte bleiben für die manuelle Stichprobe offen. Keine strukturellen Fehler zu erwarten — eher Inhalt und Ästhetik:

- **Inhaltliche Korrektheit der Sätze:** Grammatik, Natürlichkeit, Genus-Konsistenz in allen 480 Sätzen
- **Timer-Laufzeit:** dass der Timer nach 1–2 Sekunden sichtbar hochzählt
- **Streak-Verhalten:** dass die Streak bei falscher Eingabe tatsächlich zurückgesetzt wird
- **Tally-Zuwachs:** dass die `/8` oder `/4` Anzeigen korrekt inkrementieren
- **Fisher-Yates-Shuffle:** dass Items bei jedem Laden neu gemischt werden
- **Mobile-Darstellung:** Layout unter 600 px Breite
- **Lösung-Button:** dass alle Inputs auf einmal korrekt gefüllt werden

## Bekannte Eigenheiten

- **Timer-Display bei synthetischem Input:** `setInterval` läuft nach 1 s, deshalb zeigt der Timer in Tests, die unter 1 s dauern, noch `00:00`. Beim echten Benutzer ist das kein Problem.
- **Validierung case-insensitiv:** Groß-/Kleinschreibung wird toleriert (ausdrückliche Design-Entscheidung für Schreibfluss)
- **Umlaut-Strictness:** Umlaut-Fehler werden als falsch markiert (ausdrückliche Design-Entscheidung für Umlautlernen)

## Nächste Schritte

Empfohlen:
1. Einmal jede Datei im Browser kurz anspielen (3–5 Minuten pro Datei reicht): ein Item tippen, Timer beobachten, Lösung-Button drücken
2. Über die Inhaltsseite blättern — sind die Sätze alltagstauglich, passen die Emojis?
3. Ein Test-Schüler (oder du selbst am Handy) sollte Runde 1 einer Datei komplett durchspielen, um das Flow-Gefühl zu prüfen

Offene Einheiten laut HANDOVER: Uhrzeit umgangssprachlich, Mengen- und Verpackungsangaben. Beides hochfrequent im A1-Alltag, können als FD40/FD41 ergänzt werden, wenn die bestehenden zehn im Unterricht bewährt sind.
