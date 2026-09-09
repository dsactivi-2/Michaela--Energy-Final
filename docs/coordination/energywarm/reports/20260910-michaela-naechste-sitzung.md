# Startprompt: Michaela-Spezifikation prüfen und erstes Umsetzungspaket im Originalprojekt vorbereiten

Diesen Prompt in einer neuen Sitzung im Originalprojekt verwenden. Der lokale
Branch heißt `codex/michaela-specification`. Es wurde ausdrücklich nur lokal
committet; kein Remote eingerichtet, nichts gepusht und kein GitHub-PR eröffnet.

## Prompt

Nutze den Skill `livekit-agents`, um den nächsten Schritt für Michaela
vorzubereiten: Prüfe die vorhandene Spezifikation als Grundlage für die
Gesamtabnahme und arbeite das erste eng begrenzte Umsetzungspaket für das normale
Projekt `Livekit agent` aus. Der Nutzer hat für diesen Auftrag ausdrücklich
„ohne V3“ klargestellt. Diese aktuelle Aufgabenabgrenzung hat Vorrang vor dem
V3-Verweis in der früheren Fassung dieses Startprompts.
Keine erneute Befragung zu den zehn bereits entschiedenen Fachpunkten.

Original und Koordinationswurzel:
`/Users/activi/Documents/ChatGPT/Livekit agent`

Arbeitsbereich ist ausschließlich das oben genannte Originalprojekt. Kein Wechsel
in den separaten Ordner `Livekit agent Simulation V3` und keine V3-Übernahmeplanung.

Supervisor:
`/Users/activi/Documents/ChatGPT/EnergyWarm Supervisor`

### Einstieg

1. Lies geltende AGENTS.md/Overrides und das MCP-Routing. Aktiviere das Original
   in Serena und lies das Serena-Handbuch, sofern noch nicht erfolgt. Kein neues
   Onboarding. Erhalte alle vorhandenen Nutzeränderungen im Originalprojekt.
2. Prüfe den tatsächlichen lokalen Branch/Commit und Arbeitsbaum. Das
   Spezifikationspaket liegt auf `codex/michaela-specification`, sofern es nicht
   inzwischen übernommen wurde. Keine Änderungen verwerfen oder fremde Arbeit
   durch einen Branchwechsel überschreiben. Es gibt keinen vorausgesetzten
   GitHub-PR und keine Push-/Merge-Autorisierung durch diesen Prompt.
3. Lies im Supervisor PROJECTS.json, die aktuelle Worker-Routine und
   `docs/decisions/ADR-005-livekit-v3-workflow.md` samt aktuellen ADR-006-Hinweisen.
   Diese beschreiben den separaten Supervisor-Workerablauf; dieser direkte
   Auftrag setzt ihn nicht fort. Eine neue Sitzung erbt keine andere Workerrolle
   und keinen Ticketclaim. Gemeinsame Regeln nicht eigenmächtig umschreiben.
4. Lies README.md, CONTEXT.md, docs/agents/domain.md und die lokalen ADRs
   0001 bis 0005. Das lokale ADR 0005 zu Kalenderfehlern ist nicht das gemeinsame
   ADR-005 zum V3-Vorbereitungsweg.

### Maßgebliches Spezifikationspaket

Lies unter `docs/coordination/energywarm/reports/` im Original:

- `20260909-michaela-spezifikation.md`
- `20260909-michaela-spec-matrix.md`
- `20260909-michaela-spec-vertraege.md`
- `20260909-michaela-spec-nachweis.md`
- `20260909-michaela-sollablauf-workshop.md`
- `20260909-michaela-leadstatus-zur-abnahme.md`

Das Paket enthält 22 Anforderungen, 44 Situationspfade, 47 Abnahmekriterien und
acht ausdrücklich als Vorschlag gekennzeichnete gemeinsame Verträge. Prüfe
spätere Änderungen und Freigabebelege. Ein lokaler Commit, der Auftrag zum
Committen und ein bestandenes Dokumentationscheck sind keine automatische
fachliche Gesamtabnahme, Vertragsfreigabe oder Produktimplementierungsfreigabe.

### Bestätigte Fachregeln beibehalten

- Human-Angebot bei ausdrücklichem Human-Wunsch ODER aktuellem kWh-Preis,
  Grundpreis und Jahresverbrauch mindestens einer gewünschten Sparte.
- Anbieter und Zählernummer erfragen, aber nicht als Human-Terminpflicht behandeln.
  Gas-only ist erlaubt. Bei Strom/Gas reichen Kerndaten einer Sparte; fehlende
  Angaben der anderen für den menschlichen Termin vorbereiten lassen.
- Fehlende Gesprächserlaubnis bedeutet weder Interesse noch Rückrufwunsch.
- Bei Zeitmangel einmal AI-Rückruf anbieten, nur nach Zustimmung planen.
- Datenverweigerung: Einwand behandeln und Datenbedarf erklären; bei Fortbestand
  einmal Human anbieten, Zustimmung führt zur Terminvereinbarung, sonst Ende.
- Weiterhin unverständlichen Wert nach einfacherer Erklärung offenlassen,
  andere Fragen fortsetzen und normale Terminregeln anwenden.
- Kalenderausfall: mit Zustimmung Wiederanruf durch Michaela zur Terminabstimmung
  ohne festen Slot, fachlich „Wiederanrufen“ mit Notiz und erhaltenem Kontext.
- Unklarer Buchungscommit: intern klären, keine technische Kundendiskussion,
  keine unbelegte Erfolgs-/Nichtbuchungsbehauptung, keine Ersatzbuchung und
  kein neuer Klärungsrückruf.
- Bestätigte Korrekturen übernehmen/weitergeben; sichere Umbuchung selbst,
  andernfalls menschliche Übergabe. Erledigung erst nach passendem Systembeleg.
- Kontaktstopp beendet Vertrieb sofort und betrifft weitere StepEnergy-
  Vertriebsanrufe durch AI und Menschen. Bestehende Buchungsbelege erhalten.
- Weitere Regeln einschließlich Anrede, Vorstellung, Stille und Personenbindung
  stehen im Paket. Verständliche Leadstatusnamen sind keine verifizierten API-Werte.

### Konkreter Arbeitsauftrag dieser neuen Sitzung

1. Prüfe Entscheidung → Anforderung → Fall → Abnahmekriterium auf tatsächliche
   Lücken und Widersprüche. Stelle keine bereits beantworteten Fachfragen erneut.
   Technische Fragen selbst über Serena, lokale Nachweise und den vorhandenen
   offiziellen LiveKit-Docs-MCP klären. Nur einen echten neuen fachlichen
   Widerspruch dem Nutzer vorlegen.
2. Stelle den belegten Gesamtabnahmestatus und die einschlägigen gemeinsamen
   Vertragsrevisionen fest. SV01–SV08 nicht eigenmächtig als angenommen markieren.
   Prüfe insbesondere Ergebnis-/Leadabbildung, Bindung und Recovery. Gemeinsame
   Supervisor-Dateien nicht verändern.
3. Prüfe den aktuellen Quellstand, die SDK-Version und die vorhandenen Offline-
   Tests im Originalprojekt. Die bisherigen Vergleichswerte zu Original und V3
   sind historische Nachweise und kein Auftrag, V3 weiterzubearbeiten.
   Die Produktänderungen
   vor der Spezifikationssitzung sind nicht Bestandteil ihres Dokumentationscommits;
   HEAD allein bildet den geprüften Arbeitsstand daher nicht ab.
4. Bereite ein enges erstes Umsetzungspaket im Originalprojekt vor, das zwei nachgewiesene Probleme angeht:
   negative Gesprächserlaubnis wird automatisch zu Interesse/AI-Rückruf; falsche
   Person und andere ungebuchte Enden können nicht vollständig exportiert werden.
   Benenne betroffene R-/AC-IDs, Datenzustände, tatsächliche Symbole,
   bestehende Testgrenzen, minimale Deltas und gemeinsame Vertragsabhängigkeiten.
5. Lege fest, wie bestehende Buchungen, bestätigte Teilangaben und unbekannte
   Operationsausgänge bei Gesprächsende erhalten bleiben. Keine neuen Outcomes
   blind an einen unveränderten n8n-Empfänger senden. Kein pauschaler Umbau
   aufgrund der Anzahl von Tasks.
6. Erstelle einen konkreten lokalen Umsetzungsauftrag für das erste Paket mit
   Voraussetzungen, Scope, Prüffällen, SDK-Entscheidung und Rückweg. Zeige klar,
   was nach Freigabe lokal im Originalprojekt umgesetzt werden kann und was zuerst eine
   gemeinsame Vertragsannahme bzw. Ticketzuordnung benötigt.

### Grenzen und Abschluss

Diese Sitzung ist Review und Umsetzungsvorbereitung: keine Produktcodeänderung,
keine Ticket-Writes/Claims, keine fremde Rollenübernahme, kein Versand an andere
Aufgaben oder Menschen, keine neuen Provideraufrufe, Cloud-Simulationen,
Telefonate, n8n-Ausführungen oder Deployments. Keine neue Testplattform.
Vorhandene deterministische Offline-Prüfungen sind erlaubt. Ein späterer
Implementierungsauftrag braucht die passende konkrete Freigabe für das
Originalprojekt. Aus diesem Vorbereitungsauftrag folgt keine Produktänderung
und kein Auftrag zur Übernahme aus V3.

Schreibe neue Ergebnisse ausschließlich als datierten Bericht unter
`docs/coordination/energywarm/reports/` im Original. Schließe mit einer kurzen
verständlichen Erklärung ab: Was ist fachlich bestätigt, welche technischen
Verträge fehlen, ist das erste Umsetzungspaket im Originalprojekt ausführungsbereit, und welche konkrete
Freigabe bzw. Zuordnung fehlt gegebenenfalls noch? Keine historischen Testzahlen
als heutige erfolgreiche Ausführung ausgeben.

Bereite die Gesamtabnahme konkret und prüfbar vor; keine pauschale neue
Anforderungsrunde. Die Entscheidung über die fachliche Gesamtabnahme bleibt
beim Auftraggeber, gemeinsame Vertragsannahmen beim vorgesehenen Supervisorprozess.
