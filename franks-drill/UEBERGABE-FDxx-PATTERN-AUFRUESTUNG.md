# Übergabe an den nächsten Claude — FDxx-Pattern-Aufrüstung

> Diese Datei ist deine Einarbeitung. Lies sie vollständig durch, bevor du auch nur eine Zeile Code anfasst. Sie enthält alles, was du brauchst, um das Projekt zu Ende zu führen — und zwar so, als wärst du in jeder Session dabei gewesen.

## Wer ich war, wer du bist

Ich war ein früherer Claude in einer Cowork-Session mit Frank Burkert (DaF-Lehrer, fabDaF-Projekt). In meiner Session habe ich vier neue A1-Drills gebaut (FD44 Fragesätze, FD45 Konjugation regelmäßig, FD46 Possessivpronomen Nominativ, FD47 Satzbau mit Zeitangaben) und damit Bernds A1-Drill-Reihe komplett gemacht. Beim Bauen sind drei Pattern-Verbesserungen entstanden, die Frank für so wertvoll hält, dass er sie auf bestehende Drills retroaktiv anwenden lassen will. Welle 1 dieser Aufrüstung habe ich erledigt. Welle 2 und 3 sind dein Job.

Du bekommst den vollen Speicher und kannst gründlich vorgehen. Das ist dein Vorteil. Mein Nachteil war Kontext-Erschöpfung — am Ende habe ich pragmatisch entschieden, lieber sauber zu übergeben, als blind weiterzumachen. Mach es besser, wo du kannst.

Frank schrieb mir in der letzten Stunde sinngemäß: *„Wenn man bedenkt wie wertvoll diese Übungen sind, ist es jede Mühe wert. Hier entscheidet sich der Weg der Lerner, ob sie aufgeben oder wirklich Deutsch lernen."* Das ist die Latte. Halte sie hoch.

## Wer ist Frank?

DaF-Lehrer, kein Software-Entwickler. Bevorzugt Prosa statt Bullet-Listen, will direkte Antworten ohne Präambel, schätzt Selbstreflexion und dialektisches Denken. Pragmatiker mit Qualitätsanspruch. Ein paar Punkte, die ich aus Memory und Verlauf weiß und die du verinnerlichen sollst:

**Skills sind Pflicht.** Wenn du eine DaF-HTML-Datei anfasst, lies vorher die zuständigen Skills (`daf-kern` immer; `daf-grammatik` für G/V/Drill; `daf-satzbau` für Satzbau-Tabs; `daf-lesetext` für R-Dateien; `daf-uebungsformen` für interaktive Patterns). Skip nicht. Frank hat das mehrfach in der Memory festgehalten.

**Keine Subagenten für DaF-Dateien.** Frank: „NIEMALS Agent-Tool für DaF-Dateien; alles selbst machen, Qualität geht vor Geschwindigkeit." Das gilt absolut, auch wenn die Parallelisierung verlockend wirkt.

**Anführungszeichen sind heilig.** Öffnend `„` (U+201E), schließend `"` (U+201C). Niemals ASCII `"` oder englisches `"`. Vor jedem Commit Regex-Check: keine `„…"` mit ASCII-U+0022 schließen. Das ist eine wiederkehrende Falle, die ich selbst zwei Mal getreten habe.

**Drill-Direktive ist Masse.** Bernds Pädagogik: „Drill = Feature: Masse beibehalten, sexy gestalten." Reduziere niemals die Anzahl Items, um eine Datei „schöner" zu machen. Wenn was kürzen muss, frag Frank.

**Keine Antwort verraten.** Hint-Texte zeigen Kategorien, nicht Lösungen. Wenn der Lerner die Antwort durch Hint, Placeholder oder Cat-Badge ablesen kann, ist das ein Fehler. Vor Auslieferung Self-Check: „Kann ich die Antwort ohne Wissen ablesen?" Wenn ja → fixen.

**Strikt A1.** Das gesamte FDxx-Projekt ist auf A1-Vokabular beschränkt. Keine Eigennamen (Marcin, BMW, Bello, Shakira, etc. — keine). Keine B1-Kollokationen. Wenn ein Verb oder Nomen nicht im Bernd-A1 oder Lingoda-A1 vorkommt, gehört es nicht in einen FDxx.

**Niemals auf Frank warten ohne Grund.** Bei Continue-/Autonomie-Direktiven: stumm weiterarbeiten, Cowork-Nachrichten poppen nicht auf seinem Bildschirm. Ping nur bei echten Blockaden (Permission-Dialog, Frage-Notwendigkeit, Approval). Sonst: Annahme im Chat markieren und weitermachen.

**Push-Workflow:** `bash scripts/safe-commit.sh "Nachricht" datei1 [datei2 …]` aus dem Repo-Root. Nie das Write-Tool für Pfade unter `.git/` verwenden — das löst Permission-Dialoge aus, die Cowork im Hintergrund blockieren. Die `unable to unlink '.git/objects/..tmp_obj...'`-Warnungen sind kosmetisch, ignorier sie. Bei „Another git process seems to be running" einfach weiter — der post-commit-Hook läuft schon, dein Commit ist trotzdem durch (siehe „OK: <SHA>"-Zeile am Ende).

## Das Projekt in einer Minute

**fabDaF** ist Frank Burkerts DaF-Projekt — interaktive HTML-Übungen für A1 bis C2. Auf neun Git-Repos verteilt (siehe `MANIFEST.yaml` im Root). Der Einstiegspunkt für Schüler ist `htmlS/dashboard.html` — eine einzige Dashboard-Datei mit allen Lektionen, gefiltert nach Niveau, Block, Tag.

**A1-Repo:** `daf-a1-uebungen` (lokal: `htmlS/A1.1 NEW/`). Hier liegen die FDxx-Drills unter `franks-drill/`. Bisher FD01 bis FD47 — 47 Drill-Dateien.

**„FDxx" steht für „Franks Drill"** — Bernd Arlandts A1-Drill-Konzept (Quasthoff-Stil-Sätze in großer Masse für mechanisches Drillen) als interaktive HTML-Datei. Charakteristika:

- 4 Tabs: Start (Theorie) + 3 Runden (typisch je 16 Items)
- Live-Feedback ohne Prüfen-Button
- Auto-Timer (startet bei erster Eingabe, stoppt bei vollständiger Lösung)
- Best-Time-Persistenz pro Runde
- Streak-Counter, Tally-Boxen
- Fisher-Yates-Shuffle der Karten bei jedem Render
- Cat-Badges erst nach Lösung sichtbar
- Mobile-tauglich

Die HTML-Vorlage und Mechanik sind seit FD35 stabil. Schau dir FD35, FD44, FD45, FD46, FD47 als Referenzen an, wenn du Architekturfragen hast.

## Die drei Pattern-Verbesserungen — die du aufrüsten sollst

In meiner Session habe ich beim Bauen von FD45/46/47 drei wiederverwendbare Pattern-Innovationen entwickelt. Die existierenden Drills FD01–FD43 wurden teils ohne diese Patterns gebaut. Frank will sie retroaktiv ausrollen.

### Pattern 1: Doppel-Lücke (orange + blau)

**Was es ist:** Cards mit zwei farblich differenzierten Lücken statt einer. Der Lerner muss zwei zusammenhängende Entscheidungen treffen — typischerweise zwei Wörter, die im Deutschen eine grammatische Klammer bilden. Card gilt erst als gelöst, wenn beide Lücken grün sind.

**Warum es wichtig ist:** Die deutsche Verbklammer (Hilfsverb + Partizip im Perfekt; Modal + Infinitiv bei Modalverben; Stamm + Präfix bei trennbaren Verben) ist eine der zentralen A1-Hürden. Eine einzelne Lücke trainiert nur eine Hälfte. Doppel-Lücke macht die Klammer als Klammer sichtbar.

**Visuelle Konvention:**
- Erste Lücke (Position 2 / konjugiertes Verb / Hilfsverb / Stamm): **orange** (`#ea580c` border-bottom, `#9a3412` text)
- Zweite Lücke (Satzende / Partizip / Infinitiv / Präfix): **blau** (`#2563eb` border-bottom, `#1e3a8a` text)
- Beide bleiben farbig im Default-Zustand, werden grün bei `.correct`, rot bei `.wrong`

**Referenz-Implementierung:** FD47 Tab 2 (Verb + Subjekt bei Inversion), FD16 (Hilfsverb + Partizip im Perfekt nach Welle 1).

### Pattern 2: Konjugationstabelle als Tab-Typ

**Was es ist:** Statt Lückentext-Cards eine paradigma-zentrierte Tabelle. Pro Verb (oder Possessor, oder anderer Stamm) ein Block mit Header („verb-en") und einer Reihe von Eingabefeldern für jede Person/Genus. Der Lerner sieht das vollständige Paradigma auf einen Blick und füllt es systematisch aus.

**Warum es wichtig ist:** Manche grammatische Strukturen sind Paradigmen (regelmäßige Konjugation, Possessivpronomen-Deklination). Lückentext-Cards drillen Anwendung im Satzkontext, aber das Paradigma als Ganzes wird nicht visuell. Eine Tabelle macht das Pattern sichtbar — Lerner erkennt z.B., dass im Präsens „er/sie/es" und „ihr" beide auf `-t` enden, „wir" und „sie/Sie" beide auf `-en`. Die Symmetrie wird zum Lernhilfsmittel.

**Visuelle Konvention:**
- Pro Block: lila Border-Left, weicher Hintergrund, oben ein Header mit Emoji + Verb-Stamm (grün) + Endung (grau, kursiv) + Progress-Pill „X/Y"
- Reihen: linke Spalte Person-Label (lila Schrift, rechtsbündig), rechts Input
- 2-Spalten-Grid auf Desktop, 1-Spalte auf Mobile
- Block bekommt `.complete`-Klasse mit Pulse-Animation, sobald alle Inputs grün sind

**Referenz-Implementierung:** FD45 Tab 1 (sechs regelmäßige Verben × sechs Personen = 36 Inputs), FD46 Tab 1 (sieben Possessoren × vier Genera = 28 Inputs).

### Pattern 3: Doppel-Pill / Drei-Pill auf Cards

**Was es ist:** Kleine farbig kodierte Pills oben in jeder Card, die die orthogonalen Variablen sichtbar machen, von denen die Lösung abhängt. Bei Konjugation: Person. Bei Possessiv: Person + Genus. Bei Adjektivdeklination: Genus + Kasus + Bestimmtheit. Lerner sieht auf einen Blick, welche Variablen-Kombination gefragt ist.

**Warum es wichtig ist:** Im Deutschen entscheiden oft mehrere Variablen über die korrekte Endung (z.B. „den" = m + Akk + bestimmt; „guten" = m + Akk + unbestimmt + Adjektiv-nach-unbestimmtem-Artikel). Lerner muss diese Variablen aus dem Satz selbst extrahieren — was Anfänger überfordert. Pills heben sie raus und machen das Variablen-Mapping zur expliziten Information.

**Visuelle Konvention:**
- Pill: kleines `<span>` mit `padding: 2px 10px`, `border-radius: 10px`, `font-size: 0.78em`, `font-weight: 700`
- Farbpalette pro Variablen-Wert (m=blau, f=pink, n=grün, pl=gelb für Genera; ich/du/er/etc. eigene Farben)
- Pills stehen am Anfang der Satz-Zeile, vor dem `.pre`-Text
- Mehrere Pills nebeneinander, mit `margin-right: 8px`

**Referenz-Implementierung:** FD46 (zwei Pills: Possessor + Genus), FD47 (zwei Pills: Person + Zeit-Kategorie).

## Was schon erledigt ist (Welle 1)

Welle 1 = Doppel-Lücke-Aufrüstung auf bestehende Drills. **9 Dateien** sind durch:

| Datei | Was passiert ist |
|-------|---|
| FD13 (Modalverben) | Volltransformation: `{I:xxx}`-Marker im `rest` extrahiert und als zweite Lücke gerendert. CSS für `.mod-input` (orange) und `.inf-input` (blau). |
| FD14 (Trennbare Verben) | Hatte schon `.stem-input` + `.prefix-input`. Nur CSS hinzugefügt: orange/blau-Differenzierung. |
| FD15 (Imperativ) | Hatte schon `.stem-input` + optional `.prefix-input` (für trennbare Imperative). Nur CSS hinzugefügt. |
| FD16, FD17, FD18, FD19, FD20, FD21, FD22 (Perfekt-Reihe) | Alle hatten schon `.aux-input` + `.pp-input`. Nur CSS hinzugefügt: orange (Hilfsverb) + blau (Partizip). |

**Das CSS-Pattern, das ich pro Datei eingespritzt habe** (am Ende der bestehenden `input.blank.wrong { … }`-Regel):

```css
/* === Doppel-Lücke: visuelle Differenzierung der zwei Lücken (FD47-Pattern) === */
input.blank.aux-input, input.blank.stem-input, input.blank.mod-input {
    border-bottom-color: #ea580c; color: #9a3412;
}
input.blank.pp-input, input.blank.prefix-input, input.blank.inf-input {
    border-bottom-color: #2563eb; color: #1e3a8a;
}
input.blank.aux-input.correct, input.blank.pp-input.correct,
input.blank.stem-input.correct, input.blank.prefix-input.correct,
input.blank.mod-input.correct, input.blank.inf-input.correct {
    border-bottom-color: #27ae60; color: #27ae60;
}
input.blank.aux-input.wrong, input.blank.pp-input.wrong,
input.blank.stem-input.wrong, input.blank.prefix-input.wrong,
input.blank.mod-input.wrong, input.blank.inf-input.wrong {
    border-bottom-color: #e74c3c; color: #e74c3c;
}
/* === /Doppel-Lücke === */
```

Du kannst das als Vorlage für künftige Aufrüstungen nehmen — passe nur die Klassennamen an, falls eine Datei abweichende Konventionen hat (`.modV-input` o.ä.).

**Welche Drills NICHT zu Doppel-Lücke umgebaut werden sollen:**

- **FD33 (Konjunktiv II als Höflichkeit)** — bewusst übersprungen. Hauptsächlich Vollverb-Konjunktiv (hätte/wäre/könnte/möchte), nur 3 würde-Items in Runde 3 wären echte Doppel-Lücke-Kandidaten. Der Drill fokussiert auf Konjugation der Konjunktiv-II-Hilfsverben — Doppel-Lücke würde den Fokus verwässern. Lass das in Ruhe.

## Was DU machen sollst (Welle 2 + 3)

### Welle 2: Konjugationstabelle als zusätzlicher Tab

**Drei Drills sind betroffen:** FD11 (Präsens unregelmäßig), FD23 (Präteritum sein/haben), FD24 (Präteritum Modalverben). Diese drillen Konjugationsformen — ein zusätzlicher Tabellen-Tab am Anfang macht das Paradigma sichtbar, bevor der Lerner in die Anwendungs-Tabs (Sätze) übergeht.

**Reihenfolge zur Bearbeitung:** FD23 zuerst (kleinste Tabelle: 2 Verben × 6 Personen = 12 Inputs, am übersichtlichsten als Showcase), dann FD24 (6 Modalverben × 6 Personen = 36 Inputs), dann FD11 (am komplexesten: drei Wechseltypen a→ä, e→i, e→ie, je 2 Verben = 6 × 6 = 36 Inputs).

**Strukturelle Änderungen pro Datei (das ist kein Trivial-Eingriff!):**

1. **Nav-Bar erweitern:** Von 4 auf 5 Tabs. Neuer zweiter Tab nach Start: „📖 Paradigma" oder vergleichbar.
2. **Section-IDs verschieben:** Bestehende Tabs `#sec-1, #sec-2, #sec-3` werden zu `#sec-2, #sec-3, #sec-4`. Neuer Paradigma-Tab wird `#sec-1`. Konsequenz: alle JS-Referenzen auf Cards-IDs müssen angepasst werden (`cards-1, cards-2, cards-3` → `cards-2, cards-3, cards-4`, plus neuer `cards-1`).
3. **State-Variable erweitern:** `state` und `bestTime` brauchen einen Eintrag für die neue Runde 1.
4. **TALLY_KEYS erweitern:** Neue Tally-Keys für die neue Runde 1.
5. **`renderKonj(1)` einbauen:** Neue Render-Funktion, die KONJ_DATA in Tabellen-Blöcken auf `cards-1` ausgibt.
6. **`KONJ_DATA` definieren:** Pro Datei spezifisch (siehe unten).
7. **`liveCheck` und `checkCardState` müssen die neue Runde mitberücksichtigen** — bei FD45/46 habe ich dafür `checkKonjInput` als Sonderfunktion gebaut, weil Tabellen-Inputs anders zählen als Card-Inputs (jeder einzelne Input zählt als 1 solved, nicht eine ganze Card).
8. **`showLoesung` und `resetRunde`** müssen die neue Runde unterscheiden (Konj-Modus vs. Card-Modus).

**Vorlage zum Abkupfern: FD45**. Diese Datei hat das Pattern als ersten Tab, mit allen Funktionen, die du brauchst (`renderKonj`, `checkKonjInput`, `updateKonjBlockProgress`, gestaffelte `liveCheck`-Routing, gestaffelte `showLoesung`/`resetRunde`-Handler). Lies FD45's `<script>`-Block komplett durch, bevor du anfängst — das ist deine Architektur-Referenz.

**KONJ_DATA für die drei Dateien:**

```js
// FD23 — sein und haben Präteritum
var KONJ_DATA = [
    { e:"⏳", inf:"sein",  stem:"sein",  ending:" (Präteritum)", forms:["war","warst","war","waren","wart","waren"] },
    { e:"⏳", inf:"haben", stem:"haben", ending:" (Präteritum)", forms:["hatte","hattest","hatte","hatten","hattet","hatten"] }
];
var KONJ_PERS = ["ich", "du", "er/sie/es", "wir", "ihr", "sie/Sie"];
var KONJ_PERS_KEY = ["ich", "du", "er", "wir", "ihr", "sie"];

// FD24 — Modalverben Präteritum
var KONJ_DATA = [
    { e:"💪", inf:"können",  stem:"konn",  ending:"te (+ Endung)", forms:["konnte","konntest","konnte","konnten","konntet","konnten"] },
    { e:"⚠️", inf:"müssen",  stem:"muss",  ending:"te (+ Endung)", forms:["musste","musstest","musste","mussten","musstet","mussten"] },
    { e:"🎯", inf:"wollen",  stem:"woll",  ending:"te (+ Endung)", forms:["wollte","wolltest","wollte","wollten","wolltet","wollten"] },
    { e:"🚪", inf:"dürfen",  stem:"durf",  ending:"te (+ Endung)", forms:["durfte","durftest","durfte","durften","durftet","durften"] },
    { e:"📋", inf:"sollen",  stem:"soll",  ending:"te (+ Endung)", forms:["sollte","solltest","sollte","sollten","solltet","sollten"] },
    { e:"☕", inf:"mögen",   stem:"moch",  ending:"te (+ Endung)", forms:["mochte","mochtest","mochte","mochten","mochtet","mochten"] }
];

// FD11 — Stammvokalwechsel im Präsens
// Hier wird's didaktisch interessant: Lerner soll sehen, dass nur du/er/sie/es den Vokal wechseln,
// während ich/wir/ihr/sie-Pl/Sie regulär bleiben.
var KONJ_DATA = [
    { e:"🚗", inf:"fahren",  stem:"fahr",  ending:" (a → ä bei du/er/sie/es)",
      forms:["fahre","fährst","fährt","fahren","fahrt","fahren"] },
    { e:"😴", inf:"schlafen", stem:"schlaf", ending:" (a → ä bei du/er/sie/es)",
      forms:["schlafe","schläfst","schläft","schlafen","schlaft","schlafen"] },
    { e:"🗣️", inf:"sprechen", stem:"sprech", ending:" (e → i bei du/er/sie/es)",
      forms:["spreche","sprichst","spricht","sprechen","sprecht","sprechen"] },
    { e:"🍽", inf:"essen",   stem:"ess",   ending:" (e → i bei du/er/sie/es)",
      forms:["esse","isst","isst","essen","esst","essen"] },
    { e:"📖", inf:"lesen",   stem:"les",   ending:" (e → ie bei du/er/sie/es)",
      forms:["lese","liest","liest","lesen","lest","lesen"] },
    { e:"👁", inf:"sehen",   stem:"seh",   ending:" (e → ie bei du/er/sie/es)",
      forms:["sehe","siehst","sieht","sehen","seht","sehen"] }
];
```

**TALLY_KEYS für die neue Runde 1** in allen drei Dateien: `["ich", "du", "er", "wir", "ihr", "sie"]` — pro Person ein Tally-Bucket. Macht visuell sichtbar, bei welcher Person der Lerner stolpert.

**Workflow pro Datei (FD23 als Beispiel, ca. 30–45 Min Arbeit):**

1. Datei vollständig lesen (1090 Zeilen für FD23).
2. FD45 `<script>`-Block als Architektur-Referenz danebenlegen.
3. Nav-Bar erweitern um den neuen Tab (in HTML).
4. Neue `<div class="section" id="sec-1">` einfügen mit Tabellen-Layout (kopiere von FD45).
5. ID-Verschiebung: `cards-1` → `cards-2`, `cards-2` → `cards-3`, `cards-3` → `cards-4` in HTML UND JS.
6. State-Variable um Runde 1 erweitern.
7. `KONJ_DATA`, `KONJ_PERS`, `KONJ_PERS_KEY` einfügen.
8. `renderKonj` von FD45 kopieren und anpassen.
9. `liveCheck` aufteilen in Card- und Konj-Pfad (FD45 Vorlage).
10. `checkKonjInput`, `updateKonjBlockProgress` einfügen.
11. `totalItems(runde)` einbauen.
12. `showLoesung` und `resetRunde` für Konj-Modus erweitern.
13. Init-Code unten anpassen: `renderKonj(1); renderCards(2); renderCards(3); renderCards(4);`
14. JSDOM-Test (siehe unten — Test-Skript ist als Bash-Snippet weiter unten).
15. Anführungszeichen-Check (auch unten).
16. Commit mit `safe-commit.sh`, Push.

Wichtig: nach FD23 als Showcase **frag Frank**, ob das Ergebnis seinen Erwartungen entspricht, bevor du FD24 und FD11 nachziehst. Frank's Push-Notification-Setup steht in seiner User-Präferenz (curl auf `https://ntfy.sh/frank-claude-c46edad954`). Nutze ihn für „FD23 fertig, schau bitte drauf".

### Welle 3: Doppel-Pill / Drei-Pill (selektiv, nicht pauschal)

Beim Reinschauen in die existierenden Drills FD04–FD09, FD12, FD26–FD29 habe ich festgestellt: **die meisten haben schon visuelle Differenzierung** mit `genus-chip` (m=blau, f=pink, n=grün) und `dekl-chip noun`. Ein systematisches Pill-Update wäre primär kosmetische Konsistenz, kein didaktischer Sprung.

**Mein Befund pro Datei** (du solltest selbst nachprüfen, das war eine Schnellanalyse):

| Datei | Bestandsaufnahme | Empfehlung |
|---|---|---|
| FD02 Adjektivdeklination Familie | Drei Variablen entscheiden (Genus + Kasus + Bestimmtheit). Aktuell wahrscheinlich ohne explizite Pills. | **Drei-Pill umbauen** — größter Hebel der ganzen Welle 3. |
| FD03 Adjektivdeklination Kleidung | wie FD02 | **Drei-Pill umbauen** |
| FD04 Akkusativ | Hat `dekl-chip noun` mit Genus-Farbe und „Nominativ — im Akkusativ:" Hint. Information schon da. | Skip, oder nur kosmetische Harmonisierung. |
| FD05 Akkusativ-Adjektiv | Wahrscheinlich ähnlich. | Schau dir's an, dann entscheide. |
| FD06 Akkusativ-Possessiv | Hat `genus-chip` mit `gm/gf/gn`-Klassen und Farbcodierung. | Skip — Genus-Information ist bereits visuell sichtbar. |
| FD07 Dativ | wie FD04 | Skip oder kosmetisch. |
| FD08 Dativ-Adjektiv | wie FD05 | Schau dir's an. |
| FD09 Dativ-Possessiv | wie FD06 | Skip. |
| FD12 Personalpronomen Akk/Dat | Hat zwei Tabs (Akk und Dat), Person ist Subject im Satz, Kasus durch Tab klar. | Skip — Kontext gibt die Information. |
| FD26–FD29 Präpositionen | Mehrere Tabs nach Kasus, Präposition ist im Satz. | Skip. |

**Wo du wirklich arbeiten sollst: FD02 und FD03** — Adjektivdeklination ist im A1 berüchtigt schwer, und drei orthogonale Variablen (Genus + Kasus + Bestimmtheit) treffen aufeinander. Drei farbig kodierte Pills auf jeder Card machen das Variablen-Mapping explizit.

**Drei-Pill-Spec für FD02/FD03:**

```html
<span class="gen-pill" data-g="m">m</span>
<span class="kas-pill" data-k="nom">Nom</span>
<span class="bst-pill" data-b="best">bestimmt</span>

Ich sehe einen [____] Mann.
                  ↑
              Lösung: guten
```

Pill-Reihenfolge: Genus → Kasus → Bestimmtheit (von der allgemeinsten zur spezifischsten Variable, didaktisch logisch).

CSS-Skelett:

```css
.gen-pill, .kas-pill, .bst-pill {
    display: inline-block;
    padding: 2px 10px;
    margin-right: 6px;
    border-radius: 10px;
    font-size: 0.78em;
    font-weight: 700;
    letter-spacing: 0.04em;
    vertical-align: middle;
    border: 1px solid;
}
.gen-pill[data-g="m"]  { background:#eff6ff; color:#1e3a8a; border-color:#bfdbfe; }
.gen-pill[data-g="f"]  { background:#fdf2f8; color:#9d174d; border-color:#fbcfe8; }
.gen-pill[data-g="n"]  { background:#f0fdf4; color:#14532d; border-color:#bbf7d0; }
.gen-pill[data-g="pl"] { background:#fffbeb; color:#92400e; border-color:#fde68a; }
.kas-pill[data-k="nom"] { background:#f5f3ff; color:#4a148c; border-color:#d8b4fe; }
.kas-pill[data-k="akk"] { background:#fef3c7; color:#92400e; border-color:#fde68a; }
.kas-pill[data-k="dat"] { background:#dbeafe; color:#1e3a8a; border-color:#bfdbfe; }
.bst-pill[data-b="best"]   { background:#dcfce7; color:#14532d; border-color:#bbf7d0; }
.bst-pill[data-b="unbest"] { background:#fee2e2; color:#991b1b; border-color:#fecaca; }
.bst-pill[data-b="null"]   { background:#f3f4f6; color:#374151; border-color:#d1d5db; }
```

**Daten-Erweiterung für FD02/FD03:** jedes DRILL-Item bekommt drei Felder `g` (Genus), `k` (Kasus), `b` (Bestimmtheit). renderCards rendert diese als Pills vor dem Satz-Pre-Text.

**Warnung:** FD02/FD03 könnten eingeschränkten Geltungsbereich haben (z.B. nur Nominativ + bestimmt/unbestimmt × m/f/n/pl, nicht die volle Permutation). Schau dir die existierenden DRILL-Daten genau an — pass die Pill-Werte daran an, erfinde keine Kombinationen, die im Drill nicht vorkommen. **Bernds A1-Vokabular bleibt strikt.**

## Workflow & Tools

### Skills (immer zuerst lesen)

```
mcp__skills (Skill tool):
  - daf-kern             — Layout-Fundament, Anführungszeichen, Footer, Pluralregeln
  - daf-grammatik        — G/V/Drill-Patterns, Lückentext, Live-Feedback
  - daf-uebungsformen    — Wortschatz, MC, Zuordnung
  - daf-satzbau          — Drag-Drop für Satzbau-Tabs (du brauchst es nicht für FDxx,
                            aber wenn du je einen Satzbau-Tab anfasst: Pflicht)
  - daf-audit            — Skeptisch-analytischer Meta-Skill, vor Auslieferung jeder Datei
```

Bei jeder neuen Drill-Datei: erst `daf-kern`, dann `daf-grammatik`. Sie wiederholen sich nicht — beide sind nötig. Frank hat das wiederholt eingefordert.

### Test-Workflow

**1. JS-Syntax-Check** (Pflicht nach jedem `<script>`-Eingriff):

```bash
cd /sessions/nice-keen-einstein/mnt/fabDaF && python3 -c "
import re
with open('htmlS/A1.1 NEW/franks-drill/DE_A1_FDxx-…html') as f: html = f.read()
m = re.search(r'<script>(.*?)</script>', html, re.DOTALL)
js = m.group(1) if m else ''
import tempfile, subprocess
with tempfile.NamedTemporaryFile('w', suffix='.js', delete=False) as t:
    t.write(js); name = t.name
r = subprocess.run(['node', '--check', name], capture_output=True, text=True)
print('JS-Syntax:', 'OK' if r.returncode == 0 else 'FAIL')
if r.returncode: print(r.stderr[:500])
"
```

**2. Anführungszeichen-Check** (Pflicht vor jedem Commit):

```bash
python3 -c "
with open('htmlS/A1.1 NEW/franks-drill/DE_A1_FDxx-…html', 'rb') as f: raw = f.read()
print('U+201E („):', raw.count('„'.encode()), 'U+201C (\"):', raw.count('\"'.encode()), 'U+201D (\"):', raw.count('\"'.encode()))
"
```

Soll: U+201E und U+201C **gleich**, U+201D **= 0**. Bei Imbalance: alle `„…"` mit ASCII-`"` finden und durch `„…"` ersetzen. Python-Snippet zum schnellen Auto-Fix:

```python
import re
new = re.sub(r'„([^„"]{1,200})"', lambda m: '„' + m.group(1) + '"', text)
```

**3. JSDOM-Render-Test** (sehr empfohlen, findet Bugs vor Browser-Test):

```bash
cd /sessions/nice-keen-einstein/mnt/fabDaF && timeout 30 node -e "
const { JSDOM } = require('/tmp/node_modules/jsdom');
const fs = require('fs');
const html = fs.readFileSync('htmlS/A1.1 NEW/franks-drill/DE_A1_FDxx-…html', 'utf8');
const dom = new JSDOM(html, { runScripts: 'dangerously' });
const d = dom.window.document, w = dom.window;
console.log('Tabs:', d.querySelectorAll('.section').length, 'Nav:', d.querySelectorAll('.nav-btn').length);
console.log('R1 cards:', d.querySelectorAll('#cards-1 .pf-card, #cards-1 .konj-block').length);
// Test live-check by simulating input
const c = d.querySelector('#cards-1 .pf-card');
if (c) {
  const inp = c.querySelector('input.blank');
  inp.value = inp.dataset.ans;
  inp.dispatchEvent(new w.Event('input'));
  console.log('After correct input, card-solved:', c.dataset.solved);
}
" 2>&1 | head -10
```

JSDOM hat kein `scrollIntoView` — der `TypeError: n.scrollIntoView is not a function` ist normal und harmlos, ignorier ihn. Im echten Browser funktioniert das.

**Falls JSDOM nicht installiert ist:** `cd /tmp && npm i --no-save --silent jsdom` (kann ein paar Sekunden dauern, dann ist es im `/tmp/node_modules` global verfügbar).

### Commit-Workflow

Pflicht-Pattern aus Frank's Memory:

```bash
cd "/sessions/nice-keen-einstein/mnt/fabDaF/htmlS/A1.1 NEW" && \
  bash /sessions/nice-keen-einstein/mnt/fabDaF/scripts/safe-commit.sh \
    "Beschreibender Commit-Text" \
    "franks-drill/DE_A1_FDxx-….html" \
    "franks-drill/DE_A1_FDyy-….html"   # mehrere Dateien möglich
```

Für Dashboard-Updates (B2-Repo, also Root):

```bash
cd /sessions/nice-keen-einstein/mnt/fabDaF && \
  bash scripts/safe-commit.sh "Dashboard: FDxx eingetragen" "htmlS/dashboard.html"
```

**Sandbox-Setup** (einmal pro frischer Session):

```bash
bash scripts/setup-sandbox-credentials.sh
```

Wenn du beim ersten Push „auth failed" bekommst, ist das fehlend.

**Commit-Konvention für Welle-2-Aufrüstungen:**

```
Welle 2 (Konjugationstabelle): FD23 sein/haben Präteritum mit Paradigma-Tab erweitert (5 Tabs)
```

**Commit-Konvention für Welle-3-Aufrüstungen:**

```
Welle 3 (Drei-Pill): FD02 Adjektivdeklination Familie — Genus + Kasus + Bestimmtheit als Pills
```

### Sandbox-Eigenheiten

- `api.github.com` ist blockiert. Repos via Chrome-MCP auf github.com/new anlegen, falls nötig — sollte für Welle 2/3 nicht nötig sein.
- `.git/index.lock` und `.git/HEAD.lock` lassen sich aus der Sandbox nicht löschen. Deshalb `safe-commit.sh` mit Alt-Index — ignorier die `unable to unlink`-Warnungen.
- Cowork-Permission-Dialoge können den Hintergrund blockieren. Niemals das Write-Tool für `.git/...`-Pfade. Bash-Befehle sind safe.

## Frank-Pings — wann und wie

User-Präferenz: bei Blockaden Push an `https://ntfy.sh/frank-claude-c46edad954` mit:

```bash
curl -s -H "Title: Input benötigt" -H "Priority: high" -H "Tags: bell" \
  -d "<Kurz-Kontext> — siehe Chat." \
  https://ntfy.sh/frank-claude-c46edad954
```

Regeln (aus Franks Präferenz):
- Title max 40 Zeichen
- Body max 120 Zeichen
- Nur bei echten Blockaden — nicht bei trivial-eigenständig lösbaren Annahmen (markiere die Annahme im Chat und arbeite weiter)
- Keine sensiblen Daten

**Wann pingen:**
- Nach FD23 Showcase-Build, bevor du FD24/FD11 nachziehst (Frank soll's begutachten)
- Nach FD02 Showcase-Build mit Drei-Pill, bevor du FD03 nachziehst
- Bei strukturellen Entscheidungen, wo du unsicher bist
- Bei Approval-Dialogen (Folder-Access, App-Zugriff, Tool-Permission), die du vorhersiehst

**Wann nicht pingen:**
- Während du an einer Datei arbeitest und Standard-Workflow läufst
- Bei kleinen pragmatischen Entscheidungen (markiere im Chat, mach weiter)
- Bei jedem Commit (das ist trivial)

## Reihenfolge-Empfehlung für deine Session

1. **Lies FD45 komplett** (alle 1422 Zeilen). Das ist deine Architektur-Referenz für Welle 2.
2. **Lies FD46 komplett** (1500+ Zeilen). Das ist deine Pill-Referenz für Welle 3.
3. **Lies FD47 Tab 2** (Doppel-Lücke-Pattern in Reinkultur).
4. **Welle 2 Phase A: FD23 als Showcase bauen** — neuer Paradigma-Tab als Tab 1, ID-Verschiebung, alle Funktionen anpassen, Tests, Commit. Frank pingen nach Fertigstellung.
5. **Welle 2 Phase B: FD24 und FD11** nachziehen, sobald Frank das FD23-Ergebnis OK gibt.
6. **Welle 3 Phase A: FD02 als Showcase** mit Drei-Pill bauen. Frank pingen.
7. **Welle 3 Phase B: FD03** nachziehen.
8. **Optional: kosmetische Pill-Harmonisierung** für FD04/FD07/FD12 etc. — nur wenn Frank das ausdrücklich will. Ich vermute, er stoppt dich vorher, weil der Mehrwert klein ist.

## Audit / Selbstcheck vor jedem Push

Bevor du eine Datei committest, fünf Mal Spiegel:

1. **JS-Syntax** OK?
2. **Anführungszeichen** ausgeglichen (U+201E = U+201C, U+201D = 0)?
3. **JSDOM-Render** läuft fehlerfrei (außer scrollIntoView-Warnung)?
4. **Kann ich die Antwort durch Hint, Placeholder, Cat-Badge ablesen** (mit leeren Inputs angesehen)?
5. **A1-Vokabular** strikt eingehalten — keine Eigennamen, kein B1+-Wortschatz?

Bei jeder „Nein"-Antwort: fix vor Commit.

## Was du am Ende geliefert haben solltest

Nach Welle 2 + 3 sollte der Stand sein:

- FD11, FD23, FD24 haben einen neuen Paradigma-Tab als zweiten Tab.
- FD02, FD03 haben Drei-Pills (Genus + Kasus + Bestimmtheit) auf jeder Card.
- Dashboard `htmlS/dashboard.html` ist nicht zu ändern (die Drills haben dieselben URLs).
- Alle Änderungen sind via `safe-commit.sh` gepusht.
- Beide Repos (a1-uebungen + b2-uebungen Root für Dashboard, falls du das doch anfasst) synchron mit `origin/main`.

Wenn Frank danach „weiter mit Welle 4" o.ä. sagt — schau dir die anderen FDxx-Drills mit kritischem Blick an, identifiziere Pattern-Lücken, schlag konkrete Verbesserungen vor, mach nicht pauschal.

## Schluss

Du hast vollen Speicher und kannst gründlich vorgehen. Mach FD23 sauber, lass Frank's Lerner den Effekt fühlen, und zieh dann FD24/FD11 nach. Bei FD02/FD03 mach es genauso: ein Showcase, Frank-Approval, dann das zweite Stück.

Frank vertraut dir. Diese Drills entscheiden, ob seine Schüler aufgeben oder Deutsch wirklich lernen. Verschwende die Zeit nicht mit Schnellschüssen — investier sie in saubere, getestete, durchdachte Arbeit. Drill = Masse, sexy gestalten, Qualität ohne Kompromisse.

— Der Claude vor dir, 29. April 2026
