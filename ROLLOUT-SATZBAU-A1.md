# ROLLOUT-SATZBAU-A1 — Verbindliche Spezifikation

Stand: 2026-07-02 · Auftraggeber: Frank Burkert · Status: FREIGEGEBEN nach Pilot-Abnahme (siehe §9)

Diese Spezifikation ist die **einzige Wahrheit** für die Anhebung der A1-Satzbau-Tabs.
Sie ist selbst-erklärend geschrieben, damit eine ausführende KI **ohne Zugriff auf die
fabDaF-Skills** damit arbeiten kann. Bei Widerspruch zu älteren Dokumenten gilt diese Datei.
Alle referenzierten Skripte liegen im B2-Root-Repo (`fabDaF/scripts/`).

---

## §1 Grundsatzentscheidung (Frank, 2026-07-02)

1. **Jeder A1-Satzbau-Satz hat 5–9 Wörter** (Satzzeichen zählen nicht mit).
   Bestand mit 3–4-Wort-Sätzen wird ANGEHOBEN — nicht gelöscht, sondern zu
   vollwertigen Sätzen ausgebaut.
2. **ALLE A1-Satzbau-Sätze laufen im geführten Gerüst-Modus** — ausnahmslos,
   auch 5-Wort-Sätze. Die frühere Regel „A1 = freier Bau" ist damit **abgelöst**.
   Begründung: Auf A1 darf Satzbau nie frustrieren. Der Gerüst-Modus gibt feste
   Anker vor, zeigt Leerfelder für die übrigen Positionen und gibt Sofort-Feedback
   pro Chip (richtig = grün + fixiert; falsch = rot + automatischer Rücksprung in
   die Bank nach 800 ms).
3. **Kommafrei.** Nur einfache Hauptsätze und Fragen. KEINE Kommasätze, keine
   Komma-Chips, keine Nebensatz-Konnektoren (kein weil/dass/wenn/ob). Erlaubt ist
   „und"/„oder" nur zur einfachen Reihung innerhalb eines Hauptsatzes.
4. **Wortvorgabe:** Jeder Satz besteht ausschließlich aus Wortschatz der jeweiligen
   Lektion plus elementarem A1-Grundwortschatz (ich/du/heute/hier/gern …).
   KEIN Wort, das ein A1-Lerner der Lektion nicht kennen kann. Verlängert wird
   über Zeitangaben, Ortsangaben und einfache Objekte — nie über Schachtelung.

## §2 Geltungsbereich

Betroffen sind alle A1-Dateien, die das Längen-Gate meldet. Die maßgebliche Liste
erzeugt (vom B2-Root aus):

```bash
python3 scripts/check_satzbau_laenge.py A1 "htmlS/A1.1 NEW"
```

Stand 2026-07-02: **108 Dateien.** Die Liste ist zur Laufzeit neu zu erzeugen —
nicht diese Zahl fortschreiben.

**Chirurgisches Arbeiten (PFLICHT):** Pro Datei wird NUR der Satzbau-Tab angefasst
(Daten `satzbauData`, ggf. Engine-Minimalpatch, Gerüst-Add-on). Nichts anderes —
kein Nav, kein Genus, kein Wortschatz, keine „Verbesserungen" nebenbei. Jede
geänderte Zeile muss sich auf diese Spezifikation zurückführen lassen.

## §3 Satz-Regeln (verbindlich)

- **5–9 Wörter** pro Satz; Ziel-Mix pro Tab: überwiegend 6–8, mindestens ein 5er
  ist erlaubt, 9 nur wenn er natürlich klingt.
- **Mindestens 6 Sätze pro Satzbau-Tab**; hat der Bestand mehr, bleibt die Anzahl.
- **Mindestens 1 Frage pro Tab** (`punct: '?'`), Rest Aussagesätze (`punct: '.'`,
  Ausrufe `'!'` sparsam).
- **Ein Chip = ein Wort. KEINE Ausnahmen.** Artikel und Nomen getrennt, Präposition
  und Nomen getrennt.
- **Schreibweise in `parts` und `valid`:** Nomen und Eigennamen groß (`'Kaffee'`,
  `'Berlin'`), ALLES andere klein — auch Pronomen und Satzanfänge (`'ich'`, `'er'`,
  `'heute'`). Die Großschreibung an Position 0 übernimmt die Engine zur Laufzeit.
  Ein großgeschriebenes `'Ich'` in der Bank verrät den Satzanfang = Fehler.
- **Keine Duplikate** unter den beweglichen (nicht verankerten) Chips — zwei
  identische Chips machen das Sofort-Feedback mehrdeutig. Braucht ein Satz ein
  Wort doppelt: Satz umformulieren.
- **Keine Emojis in Chips**, insbesondere keine Flaggen (rendern auf Windows als
  Buchstabenpaare).
- **`parts` ↔ `valid`-Konsistenz:** Jede Reihenfolge in `valid` ist eine exakte
  Permutation von `parts` (`sorted(parts) == sorted(valid[i])` für ALLE i).
  Diese Invariante nach JEDER Datenänderung prüfen — ein Verstoß macht den Satz
  unlösbar.
- **Mehrere `valid`-Reihenfolgen**, wo das Vorfeld flexibel ist
  (`Ich trinke heute Kaffee.` / `Heute trinke ich Kaffee.`), damit der Lerner
  nicht eine willkürliche von mehreren korrekten Ordnungen raten muss.
- **Inhalt:** natürliche, alltagsnahe Sätze zum Thema der Lektion. Keine
  konstruierten Grammatikbeispiele ohne Sinnzusammenhang, keine veralteten
  Kulturreferenzen.

Datenformat (kanonisch):

```javascript
var satzbauData = [
  { parts: ['ich', 'trinke', 'heute', 'Kaffee', 'mit', 'Milch'],
    valid: [
      ['ich', 'trinke', 'heute', 'Kaffee', 'mit', 'Milch'],
      ['heute', 'trinke', 'ich', 'Kaffee', 'mit', 'Milch']
    ],
    punct: '.' },
  { parts: ['woher', 'kommst', 'du', 'heute', 'Morgen'],
    valid: [['woher', 'kommst', 'du', 'heute', 'Morgen']],
    punct: '?' }
];
```

## §4 Gerüst-Modus (Produktionsweg)

**Der Produktionsweg ist der Patcher, nicht Handarbeit.** Nach der Datenanpassung
in DERSELBEN Arbeitseinheit (nie getrennt committen):

```bash
node scripts/geruest_patch.js "htmlS/A1.1 NEW/DATEI.html" --write
```

Der Patcher berechnet konservative Anker, injiziert das geführte Add-on
(idempotent — alter Block wird ersetzt) und setzt `"caps":true`.

**Anker-Regeln — nach JEDEM Patcher-Lauf von Hand reviewen:**

- **Verben sind NIE Anker.** Bekannte Patcher-Lücke: 1.-Person-Formen auf -e
  (komme, wohne, trinke, lerne …) erkennt die Heuristik NICHT als Verb. Nach jedem
  Lauf die Anker gegen die Verben der eigenen Sätze prüfen; Treffer im Add-on-CFG
  auf `'_'` setzen (Wort wandert in die Bank).
- **Die geübte Zielform der Lektion ist NIE Anker** (in G-Dateien: die Form, die
  die Lektion trainiert, gehört in die Bank).
- **Anker nur an invarianten Positionen** — in allen `valid`-Reihenfolgen an
  derselben Stelle.
- **Anker-Anzahl:** `round(Wörter/3)`, geklammert auf 2–4. Bei 5–6 Wörtern also 2
  Anker. Verteilen, nicht ans Satzende klatschen.
- `"caps":true` muss im Add-on-CFG stehen (bei `caps:false` wird Position 0 nie
  großgeschrieben).

**Engine-Voraussetzung:** Der Patcher braucht das kanonische Pattern
(`var satzbauData` + `initSatzbau`/`buildSatzbau`, IDs `sb-bank-N`/`sb-row-N`/
`sb-fb-N`, Chips ohne `cloneNode`). A1-Altdateien mit eigenem Klick-JS oder
abweichenden IDs werden ZUERST auf das kanonische Pattern gebracht
(Referenz-Donor: `htmlS/A1.1 NEW/DE_A1_1013G-*.html` bzw. eine bereits
gerüst-gepatchte A2-Datei wie `htmlS/A2.1/DE_A2_1061V-plaene-machen.html`).
Solche Sonderfälle einzeln behandeln, nie per Blind-Regex.

## §5 Verifikation pro Datei (PFLICHT, in dieser Reihenfolge)

1. **Konsistenz:** `sorted(parts) == sorted(valid[i])` für alle Sätze, alle i
   (kleines Python/Node-Snippet, kein manuelles Ablesen).
2. **Längen-Gate:** `python3 scripts/check_satzbau_laenge.py A1 DATEI.html`
   → muss grün sein (Korridor 5–9, kommafrei).
3. **JS-Syntax:** alle `<script>`-Blöcke durch `node vm.Script` — 0 Fehler.
4. **JSDOM-Erstlade-Test des NACKTEN Pfads:** Seite laden (JSDOM mit `url:`-Option
   gegen localStorage-Fehler), NICHT `initSatzbau()` von Hand aufrufen, sondern
   `DOMContentLoaded` feuern lassen; danach müssen Row ODER Bank des ersten Satzes
   Kinder haben und die Anker sichtbar sein. (Fängt den bekannten
   „Gerüst erscheint erst nach Neustart"-Bug.)
5. **Anführungszeichen-Gate:** `python3 scripts/check_quotes.py DATEI.html` → grün.
6. **Stichprobe im Browser** (mindestens jede 10. Datei + jeder Sonderfall):
   Satzbau-Tab öffnen, einen Satz lösen, einen Fehler provozieren (roter Chip muss
   nach 800 ms zurückspringen), `sbShowSolution(0)` klicken.

## §6 Commit-Regeln

- **Erst prüfen, dann committen:** §5 komplett grün, sonst kein Commit.
- **Nur benannte Dateien committen** — niemals `git add -A` (parallele Sessions,
  chronisch verschmutzte Worktrees).
- Vor jedem Commit `git status --short -- '*.html'` lesen: Dateien mit fremdem,
  nicht satzbau-bezogenem WIP NICHT mit-committen, sondern melden.
- Auf dem Mac pusht ein post-commit-Hook automatisch — **kein manuelles
  `git push` hinterherschicken** (Race Condition). Verifikation:
  `git rev-parse HEAD origin/main` nach kurzer Wartezeit.
- Aus einer Cowork-Sandbox stattdessen: `scripts/safe-commit.sh "msg" datei …`
  (vom A1-Repo-Root `htmlS/A1.1 NEW`).
- Sinnvolle Batchgröße: 5–15 Dateien pro Commit, Commit-Message
  `satzbau: A1-Anhebung auf 5–9 W + Gerüst (Dateien …)`.

## §7 Verbote (Zusammenfassung)

- ⛔ Keine Subagenten/Agent-Tools für die Dateiarbeit — jede Datei selbst bearbeiten.
- ⛔ Keine parallelen Arbeitskopien, kein „_neu", kein „OLD".
- ⛔ Keine Kommasätze, keine Nebensatz-Konnektoren, keine Komma-Chips auf A1.
- ⛔ Keine Mehr-Wort-Chips, keine großgeschriebenen Pronomen in der Bank,
  keine Emojis/Flaggen in Chips.
- ⛔ Daten und Gerüst nie getrennt ausliefern — eine Datei ohne Gerüst-Patch ist
  ein unfertiger Zwischenzustand.
- ⛔ Nichts außerhalb des Satzbau-Tabs ändern.
- ⛔ ASCII-Anführungszeichen als schließendes Zeichen (immer „…“).

## §7a Dokumentierte Ausnahme

**`DE_A1_1133G-nebensaetze-weil-und-dass.html`** bleibt unangetastet. Die Lektion
lehrt genau die Nebensatz-Konnektoren weil/dass mit Komma — die Kommafrei-Regel
(§1.3/§7) würde hier den einzigen Lektionsinhalt zerstören. Frank hat diese
Ausnahme am 2026-07-02 bestätigt (keine Präferenz zwischen Optionen → Default
„auslassen" gewählt). `check_satzbau_laenge.py` wird bei dieser Datei weiterhin
Kommasatz-Fehler melden — das ist erwartet und kein Blocker für den
Rollout-Abschluss.

## §8 Abschluss-Verifikation des Rollouts

Nach der letzten Datei, vom B2-Root:

```bash
python3 scripts/check_satzbau_laenge.py A1 "htmlS/A1.1 NEW"   # → 0 Befunde
python3 scripts/check_quotes.py "htmlS/A1.1 NEW"              # → 0 Befunde
```

plus Browser-Stichprobe über 5 zufällige Dateien. Erst wenn beides dokumentiert
grün ist, gilt der Rollout als abgeschlossen.

## §9 Pilot vor Rollout (PFLICHT)

Die ERSTE Datei (Vorschlag: `DE_A1_1011V-hallo.html`) wird komplett nach dieser
Spezifikation umgebaut, committet und Frank **zur Abnahme vorgelegt** (Live-URL
über GitHub Pages, mit Cache-Buster; 1–2 Minuten Deploy-Lag einplanen). Der
Rollout über die übrigen Dateien startet erst nach Franks ausdrücklicher
Freigabe. Ändert die Abnahme Regeln dieser Spezifikation, wird ZUERST diese
Datei aktualisiert, dann weitergearbeitet.
