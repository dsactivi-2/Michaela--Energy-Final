# Michaela: Spezifikationsreview und erstes Umsetzungspaket im Original

Stand: 10.09.2026, Europe/Sarajevo. Direkter Vorbereitungsauftrag in Aufgabe
`01a08854-c3e8-7a20-b839-7aa4f1e17796`. Prüfzeiten unten zusätzlich in UTC.
Arbeitswurzel: `/Users/activi/Documents/ChatGPT/Livekit agent`.

**Review: PASS_WITH_GAPS. Erstes Paket konkret vorbereitet, noch nicht zur
Implementierung freigegeben. Produktabnahme: nicht bestanden/nicht erteilt.**
Die zehn Fachentscheidungen bleiben bestätigt. Eine Gesamtabnahme des
zusammengeführten Entwurfs oder Annahme von SV01–SV08 ist in den geprüften
Quellen nicht belegt. Die beiden priorisierten Fehler bestehen weiterhin.

Dieser Bericht ist das einzige neue dauerhafte Ergebnis dieser Sitzung.
Keine Produkt- oder Testdatei geändert, kein SDK-Update, Commit, Push, Claim,
Ticket-Write, Nachrichtenversand, Providerlauf oder Deployment. Keine Arbeit im
separaten V3-Ordner. Vorhandene Berichte und Nutzeränderungen bleiben erhalten.

## 1. Bewertungsbasis und Zuständigkeit

Serena-Handbuch gelesen, Original aktiviert, vorhandenes `core` gelesen, kein
Onboarding. Skill `livekit-agents` vollständig gelesen und angewendet. Geltende
AGENTS-Dateien, RTK und MCP-Routing geprüft; keine nähere Override-Datei im
Berichtspfad gefunden. Shellprüfungen über `rtk proxy`, um unveränderte Ausgaben
und kontrollierte Offline-Aufrufe zu erhalten.

Git-MCP bestätigt Branch `codex/michaela-specification` und HEAD
`bd721ea8dbb46c2f1fda08d58ef264952b216187`, Commit vom 10.09.2026 00:36:12 +02:00:
`docs: specify Michaela target workflow and prepare session handoff`.
Die lokale Git-Konfiguration enthält keine Remote-Sektion. Kein PR vorausgesetzt.

Bereits beim Einstieg unstaged: `.gitignore`, `AGENTS.md`, Koordinations-README,
die zwei Berichte `20260910-michaela-lokales-review.md` und
`20260910-michaela-naechste-sitzung.md`, `pyproject.toml`, `uv.lock`, `src/agent.py`,
`src/michaela/backend.py`, `src/michaela/state.py`, `tests/conversation_harness.py`.
Zusätzlich untracked: unter anderem `tests/test_connectivity_regressions.py` und
historische Audit-/Setup-/Koordinationsdokumente. Bewertet wurde dieser
Arbeitsbaum, nicht ein vermeintlich vollständiger Produktstand des HEAD.

Gelesene Fachbasis: [README](../../../../README.md), [CONTEXT](../../../../CONTEXT.md),
[Domain](../../../agents/domain.md), lokale ADRs 0001–0005 sowie
[Spezifikation](20260909-michaela-spezifikation.md),
[Matrix](20260909-michaela-spec-matrix.md),
[Vertragsvorschläge](20260909-michaela-spec-vertraege.md),
[historischer Nachweis](20260909-michaela-spec-nachweis.md),
[Workshop](20260909-michaela-sollablauf-workshop.md) und
[Leadstatusentwurf](20260909-michaela-leadstatus-zur-abnahme.md).
Der nachträglich präzisierte lokale Startprompt stimmt mit dem eingefügten
Nutzerauftrag hinsichtlich „Original, ohne V3, nur Vorbereitung“ überein.

Im Supervisor wurden PROJECTS.json, Worker-Routine, Domain, CONTRACTS.md,
DECISIONS.md, ACCEPTANCE.md und ADR-005/006 gelesen. Der dort registrierte
Workerablauf wird hier nicht fortgesetzt. Kein Guard erworben, keine fremde
Taskrolle oder Ticketzuordnung übernommen. Die direkte aktuelle Nutzeranweisung
begrenzt diesen Auftrag auf das Original; gemeinsame Dateien werden deshalb
nicht umgeschrieben. Lokales ADR 0005 regelt Kalenderfehler, gemeinsames ADR-005
einen separaten Arbeitsablauf.

Hivemind `rules list` und `goal list --mine`: nicht angemeldet. Expliziter lokaler
read-only Fallback: `~/.deeplake/memory/index.md` fehlt. Verbindliche Projekt- und
Sitzungsdokumente verwendet; kein Login, keine Memoryänderung.

## 2. Gesamtabnahme: konkrete Feststellungen

Das Paket definiert jeweils genau einmal **R01–R22, M01–M44, AC01–AC47 und
SV01–SV08**. Diese Strukturprüfung belegt vorhandene IDs, keine Produkterfüllung.
Die fachlichen Präzisierungen sind konsistent aufgelöst: B11 ersetzt die
pauschalen älteren Human-Schranken, B25 ersetzt B21, B27/B28 schließen die früher
offenen Fortsetzungen bei Verweigerung und Nichtverstehen. F01–F10 werden nicht
erneut zur Entscheidung gestellt.

### Rückverfolgung und Abnahmeumfang

Die folgende Zuordnung ergänzt die Matrix um Querschnittsprüfungen. Sie ist eine
Reviewauflage zur Abnahme, keine nachträgliche Änderung der Quelldokumente.
Alle AC bleiben Sollkriterien; die heutigen 79 Regressionen sind kein AC-PASS.

| R | Entscheidung / Quelle | Situationen | AC / Revieweinschätzung |
|---|---|---|---|
| R01 | B01/B16/B17, ADR 0004 | M01 plus Anredewechsel quer durch M17/M24/M36 | AC01/02; AC02 braucht expliziten Querschnittsfall. |
| R02 | B03/B06, ADR 0002 | M03–M05 | AC03/04; Fehler frisch reproduziert. |
| R03 | B04/B05/B18 | M11–M16, M44 | AC05–07; Klärung, Ende und Kontaktstopp getrennt. |
| R04 | B13/D05, ADR 0001 | M01/M02/M07–M10 | AC08–10; Dritthinweis und eigene Personenbindung unterscheiden. |
| R05 | B08/B14/B15/B19 | M16–M18/M22/M31 | AC11–13; Arbeitspreis-/Spartenlücken bleiben spätere Produktarbeit. |
| R06 | B20/B27, ADR 0002/0003 | M20 | AC14; einmal Human, bei Ablehnung Ende. |
| R07 | B24/B28, ADR 0004 | M19 | AC15; unklar lassen, übrige Fragen fortsetzen. |
| R08 | B11/B14/B15/B19 | M06/M18/M20/M22 | AC16–18; Human-Wunsch ODER Kerndaten einer gewünschten Sparte. |
| R09 | B02/B06/B11/B12 | M05/M21/M23/M26 | AC04/19; AI-Zustimmung und Zweck eigenständig. |
| R10 | D01/D02, ADR 0001/0003 | M02/M24/M25/M29 | AC20–23; Bindungs-/Belegvertrag nicht vollständig. |
| R11 | B12 | M26/M28 | AC24; leere erfolgreiche Suche ist kein Kalenderfehler. |
| R12 | B25, lokales ADR 0005 | M27/M40 | AC25/26; Wiederanruf ohne Slot benötigt Annahmevertrag. |
| R13 | B22 | M29/M30/M39/M44 | AC27–29; unklar bleibt intern, keine Ersatzaktion. |
| R14 | B26/D04 | M32/M33/M44 | AC30/31; Kundenrevision und Empfängerbeleg getrennt. |
| R15 | B26 | M34/M35/M40 | AC32–34; unklarer Umbuchungscommit beweist nicht fortbestehende Aktivität des alten Termins. |
| R16 | Direkter Gesamtauftrag | M31/M32/M36/M44 | AC35/36; Mehrfachwerte und bestätigte aktuelle Revision erhalten. |
| R17 | B23/D06/D07 | M37/M41/M42 | AC37–39; Betriebs-/Telefonieanteile separat, keine neue Retry-Politik. |
| R18 | D08, ADR 0001 | Alle terminalen M, besonders M02/M07/M09/M28/M37–M44 | AC29/40–42; Ergebnisweg ist heute unvollständig. |
| R19 | B22/B25/B26/D08 | M30/M39/M40/M44 | AC28/29/41–43; dauerhafte Recovery fehlt. |
| R20 | B12/B25 | M43 | AC44/45; AC44 sprachlich präzisieren, siehe unten. |
| R21 | ADR 0001/Projektregeln | Jeder M-Pfad mit zwei Calls, zusätzlich M44 | AC46 als expliziten Querschnitt aufnehmen. |
| R22 | Historischer gemeinsamer ADR-005-Arbeitsweg | Kein eigener Kundenfall | AC47 für diesen Originalauftrag nicht anwendbar; lokale Ersatzprüfauflage unten. |

### Reviewauflagen vor Gesamtabnahme

1. **Aktueller Arbeitsumfang:** R22/AC47 sowie U1–U8 enthalten noch den früheren
   Vorbereitungs-/Übernahmeweg. Für diesen direkten Originalauftrag gilt stattdessen:
   Originalbasis und Nutzeränderungen sichern, auf dessen Lockstand prüfen, nur
   ausdrücklich genehmigte lokale Deltas bearbeiten. Kein Doppelvergleich und
   keine Übernahmeplanung. R22/AC47 nicht als bestanden markieren; außerhalb
   dieses Auftrags bleibt der gemeinsame Supervisorablauf unberührt.
2. **AC44 eindeutig formulieren:** „bei Terminabstimmung nicht abgeschlossene
   Tarifaufnahme wiederholen“ ist missverständlich. Präzisierung gemäß B12,
   lokalem ADR 0003 und M43: „Bei Folgezweck Terminabstimmung die Terminabstimmung
   fortsetzen; bereits abgeschlossene Tarifaufnahme nicht wiederholen.
   Datenergänzung fragt nur tatsächlich offene Angaben.“ Keine neue Fachwahl.
3. **Explizite Matrixabdeckung:** AC02 und AC46 fehlen als direkte AC-Referenz in
   den Matrixzeilen; AC47 ist eine technische Freigabeprüfung außerhalb eines
   Kundenfalls. Ergänzende Prüffälle: Siezen nach Wechsel Erfassung → Termin →
   Abschied; zwei parallele synthetische Calls mit verschiedenen Teilständen,
   Endgründen und Buchungen. Die bestehende Querschnittsregel allein nennt diese
   beiden Kriterien nicht ausdrücklich.
4. **Nachbuchungsänderung präzise lesen:** Die Kurzfassung im Leadstatusentwurf
   („sonst … menschliche Bearbeitung“) darf nach unklarem Umbuchungscommit keine
   unabhängige Ersatzbuchung auslösen. SV06/M30/M44 sind eindeutiger: alten
   **Beleg** behalten, aktuelle Wirkung als unklar erhalten, denselben Vorgang
   intern klären. Die Übergabe bei fehlender sicherer Umbuchungsfähigkeit ist
   bereits entschieden; keine erneute Kundenbefragung nötig.
5. **Geltungsbereich der Gesamtabnahme:** Dieses Paket beschreibt Michaela
   Outbound. Es ersetzt nicht die gemeinsame EnergyWarm-Gesamtabnahme mit
   Inbound und Call-Controller gemäß ACCEPTANCE.md. Aus D05–D07 übernommene
   Erwartungsbeschreibungen sind keine im Original vorhandenen Funktionen.

Kein neuer ungelöster fachlicher Widerspruch wurde gefunden, der eine erneute
Entscheidung zu den zehn Fachpunkten verlangt. Offen sind die Abnahme des
konsolidierten Umfangs samt diesen Präzisierungen und technische Verträge.

## 3. Gemeinsame Verträge und tatsächliche Ticketlage

[CONTRACTS.md](</Users/activi/Documents/ChatGPT/EnergyWarm Supervisor/CONTRACTS.md>)
meldet weiterhin „noch keine neue Vertragsrevision freigegeben“; das vorhandene
Verzeichnis `contracts/` ist leer. In den durchsuchten gemeinsamen Markdownquellen
kein Annahmebeleg für SV01–SV08 oder das Michaela-Spezifikationspaket gefunden.
Die gezielte native Linear-Abfrage bestätigte Team und Projekt aus PROJECTS.json,
32 nicht archivierte Tickets, keine weitere Seite. Stand dieser Sitzung:

| Ticket | Gelesener Zustand / Bedeutung |
|---|---|
| [ACT-29](https://linear.app/activi/issue/ACT-29) | In Progress; Zielumgebung/Deploymentherkunft. Blockiert ACT-30. |
| [ACT-30](https://linear.app/activi/issue/ACT-30) | Backlog; keine Vertragsrevision beschlossen; Kommentarabfrage leer, vollständig. |
| [ACT-41](https://linear.app/activi/issue/ACT-41) | Done; Vergleich/Regression, keine Freigabe dieses Umsetzungspakets. |
| [ACT-42](https://linear.app/activi/issue/ACT-42) | Backlog; terminale Enden. Native Blocker ACT-41 und ACT-30; letzterer offen. |
| [ACT-43](https://linear.app/activi/issue/ACT-43) | Backlog; Buchung/Bindung/Recovery. Gleiche native Blocker. |

ACT-42/43 enthalten noch die feste alte Task-ID und ADR-004-Ausführungspolicy.
ADR-006 und PROJECTS.json erlauben dem Altworker nur ACT-41. Eine neue Zuordnung
muss der Supervisor/Verteiler vor einer ticketausführenden Sitzung konsistent
herstellen; der Tickettext ist kein Claim für diese Aufgabe. Für Arbeiten im
Original muss auch der konkrete zulässige technische Root ausdrücklich zum
Auftrag passen. Keine stillschweigende Umdeutung des bisherigen Workertickets.

| Vorschlag | Gemeinsame Entscheidung | Voraussetzung für das erste Paket |
|---|---|---|
| SV01 Ergebnis/Lead/Kontaktstopp | R-D-03/05/07 | Endgrund, Wunsch, Buchung und Lieferung trennen; versionierte Leadabbildung ohne positives Ersatzoutcome. **Vor realer Exportanbindung erforderlich.** |
| SV02 Bindung/Teilstand/Kontext | R-D-02/07 | Vertrauenswürdige Call-/Lead-/Personenzuordnung; sichere technische Ergebnisse ohne Lead; Teilstand und Herkunft. **Vor entsprechender Übergabe erforderlich.** |
| SV03 Angebot/Buchungsbeleg | R-D-02/04/08 | Passenden vorhandenen Beleg erhalten; neue korrelierte Quittung erst nach beidseitiger Annahme. Voller Angebotsumbau außerhalb P1a. |
| SV04 Wiederanruf ohne Slot | R-D-03/05/07 | Nicht in P1a implementieren; kein Rückrufauftrag aus allgemeinem Ende oder unklarer Buchung. |
| SV05 Operation/Lieferung/Recovery | R-D-02/05/06/07 | Speicherquittung, Deduplizierung, gleiche Operation bei Timeout, dauerhafter Owner. **Vor dauerhafter Ergebnis-/Operationsgarantie erforderlich.** |
| SV06 Update/Umbuchung | R-D-02/04/05/07/08 | Außerhalb P1a; vorhandene Belege und Korrekturwünsche erhalten, keine neue Umbuchung. |
| SV07 menschliche Übergabe | R-D-03/05/07 | Außerhalb P1a; keine behauptete Übergabe ohne angenommenen Empfänger. |
| SV08 Lifecycle | R-D-01/02/05/06 | Call-/Job-Korrelation und späteres Ergänzen nach Sitzungsende; vor externem ungebundenem Abschluss/Recovery nötig. |

R-D-02/03/04/06/07 sind laut DECISIONS.md offen; R-D-01/05/08 nur
teilentschieden. Kein Vorschlag erhält durch diesen Bericht eine Versionsnummer.
SV01/02/05 und der betroffene SV08-Teil bilden die minimale gemeinsame
Ergebnisgrundlage; SV03 kommt bei Buchungsquittung/Korrelation hinzu.
Das bedeutet nicht, dass sämtliche SV04/06/07-Funktionen vor lokalen P1a-Fakes
gebaut werden müssen. Bestehende native Blocker werden dennoch nicht umgangen.

## 4. Frisch belegte Fehler und minimale Änderungsstellen

Root Cause: Negative Gesprächserlaubnis dient an mehreren Stellen als Ersatz
für einen ausdrücklichen Rückrufwunsch. Gleichzeitig erzwingen abschließende
State- und Payloadprüfungen ein Verkaufsoutcome und schließen verschiedene
ungebuchte oder mit Buchung koexistierende Endgründe aus.

Die bestehenden zwei Minimal-Repros wurden unverändert und nur im Original
ausgeführt. Ergebnis:

```json
{"permission_false_outcome":"interessiert","permission_false_appointment_kind":"ai","wrong_person_export":"final result requires an explicit outcome"}
```

Der Repro beendet sich mit Exit 0, weil er **Fehler beobachtet**, nicht weil AC03
oder AC40 erfüllt wären. Er beweist keine tatsächlich ausgelöste Kundenbuchung.

| Aktuelle Symbole | Tatsächlicher Befund | Minimales späteres Delta |
|---|---|---|
| `PermissionTask.on_enter`, `record_permission` in `src/agent.py` | Zeitmangel/negativer Bool erzeugt pauschale Rückrufansage; auch nicht erkannte Antwort wird negativ. | Erlaubnis ungeklärt/ja/nein erhalten; fehlende Erlaubnis kurz klären; Zeitmangel → einmal Angebot, Antwort separat aufnehmen. Stoppsignal beendet unmittelbar. |
| `_rueckruf_only`, `_skip_collection`, `_skip_after_wrong_person`, `MichaelaFieldTask` | `permission=False` aktiviert Rückruflogik bzw. überspringt Erfassung; Stoppschranken nur teilweise vorhanden. | Rückrufpfad ausschließlich bei ausdrücklich angenommenem AI-Wunsch; Erfassung bei Zeitmangel sperren, Entscheidung/Ende erlauben. Terminalität und Kontaktstopp in allen abhängigen Pfaden prüfen. |
| `OutcomeTask`, `GrundTask._rueckruf_complete_now`, `TerminArtTask`, `TerminStartTask` | Rückrufprompt/Artwahl und erfundener Grund können die alte Ableitung erneut herstellen. | Keine automatische Interessens-/AI-/„keine Zeit“-Ableitung; gewünschte Art getrennt von tatsächlich gebuchter Art. Kalenderzugriff erst nach passender Zustimmung. |
| `_pack_dc_results` (`agent.py:554`) | Negativer Permissionzweig setzt `interessiert`/`ai`; falsche Person entfernt Outcome. | Reiner Snapshot aus aktuellem Fachzustand, ohne Wunsch/Erfolg zu ergänzen; Identitätsgrund erhalten. |
| `IdentitaetTask.record_identitaet` | `nicht_da`/`verwaehlt` vorhanden; setzt generischen Abbruch erst nach Abschiedsrede. | Vor optionaler Rede terminalen Grund und Bindungsstatus sichern; beide Fälle exportierbar unterscheiden. Keine neue fremde Personenbindung in P1a. |
| `CallState.validate_final` (`state.py:199`), `build_final_payload` (`result.py:9`) | Outcome Pflicht; `interessiert` verlangt AI-Buchung; nichtterminliche Outcomes verbieten Buchung; fehlende Leadbindung verhindert Payload. | Fachabschluss unabhängig validieren; Buchungsdaten separat konsistent prüfen. Interner Snapshot von Wireabbildung trennen; ungebundene Fälle nie an beliebige Lead-ID schicken. |
| `DefaultAgent.on_enter`, `_finish_data_collection` (`agent.py:1866`) | Bei TaskGroup-Abbruch werden nur Identitätsresultate und öffentlicher State zusammengeführt. | Aktuellen bestätigten Teilstand bei Aufnahme sichern; Abschluss aus diesem Zustand auch ohne vollständiges TaskGroup-Ergebnis. |
| `JahresgrundpreisTask.record_jahresgrundpreis`, weitere `record_*`, `AktuellerVersorgerTask.edit_aktueller_versorger_list` | Einzelwerte nur Taskresultat bzw. lokale Anbieterliste; unvollendete Tasks verlieren Daten im Abschluss. | Schon akzeptierte Einzelangaben vor `complete` call-lokal speichern; Zwischenstand der Liste vor Abschluss ebenso. Keine neue Vollständigkeit oder Sparte erraten. |
| `_http_tool_book_termin` (`agent.py:1946`), `CallState.confirm_booking` | Positiver Body wird geprüft, Event-ID aber nicht im State gehalten; Fehler verlieren die Unterscheidung möglicher Wirkung. | Nur vorhandenen geprüften Beleg behalten; Versuch vor Await referenzieren, nach möglichem Versand Fehler als unklar erhalten. Kein Statusdienst oder neuer Retry in P1a. |
| `_on_session_end` (`agent.py:2049`), `export_final_result`, `N8nEnergyBackend.save_result` | Exportbody nicht fachlich geprüft; fehlende Ausnahme ergibt „ok“. Reportfehler nur für RuntimeError abgefangen; kein dauerhafter Recoveryweg. | Fachabschluss vor optionalem Sessionreport; bekannte Fehler und doppelte Endevents testen. Lieferzustand separat; neue Quittungsprüfung erst gegen vereinbarte Revision, im Fake vorab vorbereitbar. |

Ein bloßes Löschen des Fallbacks in `_pack_dc_results` behebt weder die
Rückrufansage noch die nachfolgenden Taskzweige. Ein bloß neues Outcome-Enum
behebt weder fehlende Teilstände noch unklare Buchung oder Empfängerkompatibilität.
Ein pauschaler Taskumbau ist für diese Fehler nicht erforderlich.

## 5. Erstes Paket P1: unabhängige Erlaubnis und vollständiger Fachabschluss

**P1a: lokal nach ausdrücklicher Freigabe umsetzbare Vorbereitung mit Fakes.**
**P1b: Exportintegration erst nach gemeinsam angenommener Revision und Zuordnung.**
P1a allein ist weder vollständige produktive Exportreparatur noch Freigabe für
einen laufenden Agenten. Diese Teilung hält das erste Paket prüfbar, ohne
Backendfähigkeiten vorzutäuschen.

### Zustandsumfang und Übergänge

Die Namen unten bezeichnen lokale Fachdimensionen, keine neuen Wirefelder/Enums.

| Dimension | Erforderliche Unterscheidung / Übergang |
|---|---|
| Erlaubnis | ungeklärt / jetzt ja / jetzt nein; kein Rückruf- oder Interessensschluss. |
| Situation | ungeklärte Bereitschaft, Zeitmangel, offener Einwand, bestätigte Ablehnung, Ende jetzt; Kontaktstopp zusätzlich mit sofortiger lokaler Wirkung. |
| Interesse | unbekannt / ausdrücklich geäußert / nach Klärung abgelehnt; keine Pflichtklassifikation. |
| Folgewunsch | keiner/ungeklärt, Human ausdrücklich, AI angeboten, AI angenommen oder abgelehnt; AI-Angebot einmal, Zweck nur aus tatsächlichem Wunsch. |
| Abschluss | läuft oder tatsächlicher Endgrund; mindestens fehlende Erlaubnis ohne Folgewunsch, Zielperson nicht da, falscher Anschluss, bestätigte Ablehnung, Ende auf Wunsch, Stille, Kundentrennung, technischer Abbruch, ungebuchter Terminwunsch. Vorhandene Mailbox-/Keine-Antwort-Werte erhalten. |
| Teilstand | Aktuelle im vorhandenen Record-/Listenpfad bestätigte Werte, Herkunft und offene Felder; Snapshot unabhängig von Taskabschluss. Unbestätigte LLM-Vermutung zählt nicht als Wert. |
| Buchung/Operation | kein Versuch, vorbereitet, versandt/ausstehend, bestätigt mit vorhandenem Beleg, sicher nicht ausgeführt oder unklar. Wunsch und gewählte Art nicht als bestätigte Buchung verwenden. |
| Lieferung | vorbereitet, ausstehend, angenommen nur mit Beleg, sicher abgelehnt, unklar oder wegen fehlender kompatibler Empfängerrevision blockiert. |

Bei bloßem `permission=False` bleibt Interesse unbekannt und AI ungewünscht.
Bei belegtem Zeitmangel genau einmal fragen, ob Michaela zurückrufen soll;
ohne Antwort keine Planung, bei Nein Ende, bei Ja nur AI-Terminplanung.
Das Ja zum Rückruf bestätigt noch keinen Slot. Ausdrücklichen Human-Wunsch
bei Zeitmangel erhalten, nicht in AI umwandeln. Ein erstes „Kein Interesse“ darf
kurz geklärt werden; bestätigtes Nein oder Auflegewunsch überspringt Folgeangebote.

P1a ergänzt die kleinsten Record-/Entscheidungspfade innerhalb der bestehenden
Tasks, statt eine neue generelle Dialogplattform zu bauen. Natürliche
Formulierungswahl bleibt durch Offline-Tests nur begrenzt bewiesen.

### Erhaltungsregeln am Gesprächsende

1. **Buchung ist unabhängig vom Endgrund.** Gebuchter Slot, Art, Start/Ende und
   tatsächlich empfangener Beleg bleiben bei späterem Nein, Kontaktstopp,
   Auflegen oder Fehler erhalten. Wunschkorrekturen dürfen diese Felder nicht
   überschreiben. Fehlende historische Event-ID als fehlend kennzeichnen,
   niemals aus Zeit/Slot rekonstruieren. Kontaktstopp ist keine Stornoquittung.
2. **Teilstand vor Taskende sichern.** Die bestehenden Record-Tools schreiben
   bestätigte Daten vor ihrer Completion; Listenänderungen sichern ihre bereits
   aufgenommenen Einträge. `on_task_completed` kann ergänzen, erfasst aber keine
   unvollendete Aufnahme. Finale Serialisierung erzeugt eine unabhängige Kopie,
   keine Referenz auf später weiter mutierte Listen. Spätere bestätigte Revision
   gewinnt; aus den heutigen ungetrennten Tarifstrings keine Sparte erfinden.
3. **Unklare Wirkung konservativ erhalten.** Versuch und Payloadbezug vor dem
   Backend-Await setzen. Antwortverlust/ungültige Antwort nach möglichem Versand
   bedeutet unklar. Der derzeitige generische BackendError beweist keine sichere
   Nichtausführung. Alte bestätigte Belege und neue unklare Operation koexistieren.
   Keine zweite Buchung, kein neuer Schlüssel zur Klärung, kein Klärungsrückruf.
4. **Ein logischer Abschluss, korrelierte Ergänzungen.** Endgrund und Snapshot
   vor Abschiedsrede/Room-Cleanup sichern. Verspäteter Beleg ergänzt die
   bestehende Operation; keine zweite Verkaufsentscheidung und keine Rücksetzung
   neuerer Kundenrevisionen. In P1a mit Fakes prüfen, extern erst mit SV05/SV08.
5. **Prozessverlust bleibt Integrationsgrenze.** CallState, `asyncio.shield` und
   das optionale redigierte Journal sind kein dauerhafter Fachspeicher. P1a
   verspricht Zustandserhalt nur innerhalb der geprüften lokalen Laufzeit.
   Wiederherstellung nach Prozessneustart benötigt vor externer Wirkung dauerhaft
   registrierte Operationen beim vereinbarten Owner. Keine provisorische PII-Datei
   oder neue lokale Warteschlange als Ersatz.

### Empfängergrenze

Den bestehenden `N8nEnergyBackend` nicht mit neuen Outcomes aufrufen. Für P1a
einen internen vollständigen Snapshot und eine ausdrücklich als Vorschlag
gekennzeichnete Fake-Annahme prüfen. Die reale Wireabbildung bleibt auf den
belegten Altumfang beschränkt. Eine neue Kombination darf weder auf `abgelehnt`
noch `interessiert` umetikettiert werden, um die alte Validierung zu passieren.
Fehlende Empfängerunterstützung muss als blockierte Lieferung sichtbar bleiben;
das ist kein erfolgreicher Export und verhindert einen Rollout von P1a allein.

P1b benötigt versioniertes Schema mit Endgrund/Teilstand/Buchung/Operation,
definierte Null- und Fehlerregeln, sichere Bindung bzw. Call-/Job-Fallback ohne
Lead, positive Ergebnisquittung und dieselbe Revision auf beiden Seiten.
Empfänger zuerst prüfen und unterstützen lassen. Dann den Agentadapter anbinden,
synthetische positive/negative Vertragsbeispiele und separat autorisierte
Integrationsfälle nachweisen. Kein eigener n8n-Workflowentwurf in diesem Auftrag.

## 6. Konkrete Prüfaufträge für P1a/P1b

Primär R02/R09/R18; R03/R04 für End- und Identitätsgrenzen; R10/R13/R14/R19/R21
nur soweit nötig, um beim Abschluss bestehende Wirkungen und Teilstände zu
schützen. Kein Anspruch, diese ganzen Anforderungen durch P1 zu erfüllen.

| Fall | Auslöser / Grenze | Erwartete Beobachtung | AC |
|---|---|---|---|
| P1-01 | Echter Permission-Record: nein, kein Folgewunsch | Kein Interesse/AI/Grund erfunden, keine Kalender- oder Buchungsaktion; abschließbarer Snapshot. | AC03/40 |
| P1-02 | Zeitmangel; Angebot offen/Nein/Ja, jeweils eigener Fall | Genau ein AI-Angebot; offen/Nein null Planung; Ja nur passende Planung, keine Buchung ohne Slotbestätigung. | AC04/19/20 |
| P1-03 | Erstes Nein, bestätigtes Nein, Auflegewunsch, Kontaktstopp | Kurze Klärung nur beim offenen Einwand; danach Ende. Stopp verhindert neue Vertriebsaktionen und übersteht Taskwechsel. | AC05/07 |
| P1-04 | Identitäts-Record `nicht_da` bzw. `verwaehlt`, danach Ende | Unterschiedlicher tatsächlicher Grund, keine Zustimmung/Termin, Originalbindung unverändert, vollständiger Fake-Abschluss. | AC08/10/40 |
| P1-05 | Fehlende Call-/Leadbindung | Interner technischer Abschluss mit vorhandener sicherer Korrelation; kein Leadwrite. Externer Fallback bleibt Vertragsgate. | AC21/40/42 |
| P1-06 | Human- oder AI-Wunsch, kein akzeptierter Slot | Wunsch ungebucht erhalten, kein positives Buchungsoutcome und kein neuer Wiederanrufauftrag. | AC19/24/40 |
| P1-07 | Record-Tool für Wert, Listen-Teilaufnahme, dann TaskGroup-Abbruch | Tatsächlich erfasste Teilwerte im Snapshot/Fake-Ergebnis; nicht erst nachträglich Test-Endstate setzen. | AC40/42, Teil AC35/36 |
| P1-08 | Zweite bestätigte Korrektur vor Ende; verzögerte ältere Antwort | Letzte bestätigte Angabe bleibt aktiv; bekannte alte Belege separat. Keine behauptete Backendänderung. | AC31/43 |
| P1-09 | Bestätigte Human-/AI-Buchung, danach Ablehnung/Stopp/Disconnect | Buchungsbeleg und Endgrund koexistieren; null zusätzliche Buchungs-/Stornoaktionen. | AC07/29/40 |
| P1-10 | Fake-Buchungsversuch ausstehend, Timeout/ungültige Antwort, dann Ende | Operation unklar samt Wunsch/Bestätigung erhalten; kein neuer Versuch oder Klärungsrückruf. Späteren Beleg passend ergänzen. | AC27/29/42 |
| P1-11 | Doppelte/concurrent Endevents, Sessionreportfehler, fehlende TTS | Fachsnapshot unabhängig von Rede/Report; ein logischer Abschluss. Fake-Zählung zeigt keine zweite Buchung. | AC40/42 |
| P1-12 | Ergebnisantwort negativ, HTTP-200-Fehlerbody oder Timeout | Kein Speichererfolg; Lieferung abgelehnt/unklar nach vorgeschlagenem Vertrag. Realer Nachweis erst P1b. | AC41 |
| P1-13 | Neue Ergebnisrevision gegenüber unverändertem Empfänger | Null Versand des neuen Formats; Lieferblock sichtbar, keine positive Legacy-Umetikettierung. | AC03/40/41 |
| P1-14 | Zwei parallele synthetische Calls mit unterschiedlichen Enden | Keine Daten-/Belegverwechslung; Diagnostik redigiert. | AC46 |
| P1-15 | Vorhandene echte Tooltests für Bindung/angebotenen Slot/Quittung | Schutz vor unangebotenem/artfremdem Slot und ungültigem Beleg bleibt wirksam. | AC20–23, Teilnachweis |

P1-01/04 zuerst als erwartbar rote Regressionen. Den bestehenden
`test_no_time_creates_ai_callback_outcome` in „ohne Zustimmung“ und „explizit
angenommener Rückruf“ aufteilen. Den Schutz vor erfundenem Outcome behalten;
`test_wrong_person_scenario_cannot_invent_an_outcome` und
`test_final_payload_requires_explicit_closed_outcome` dürfen nach dem Fix nicht
weiter einen unmöglichen Abschluss als erwünschtes Verhalten festschreiben.
`test_final_outcome_and_booking_must_match` in separate Fachabschluss- und
Buchungsinvarianten überführen; fehlerhafte Buchungsbelege weiter abweisen.

Vorhandene höchste deterministische Grenze: echte Agent-/Task-Tools mit
CallState/FakeEnergyBackend bis Payload und Session-Endhook. Der
ConversationHarness setzt in `finish(outcome)` Zustand selbst und prüft keine
Permission-Äußerung oder echte TaskGroup-Fortsetzung. `book` im Harness ersetzt
auch keinen Test der vollständigen Agent-Quittungsprüfung.
`test_session_end_exports_real_sdk_usage` prüft echte SDK-Usage-Datentypen an
einem Fake-Backend, keine Modellaufrufe. Der Testname „exported_once“ allein
beweist keine parallele oder serverseitige Deduplizierung.

Für P1b kommen beidseitige Schemafälle, Annahmebeleg nach Antwortverlust,
ungebundener technischer Abschluss, unveränderte historische Buchung,
Kontaktstopp plus Buchung sowie dauerhafte Recovery nach Jobneustart hinzu.
AC28/41/42 auf Integrationsebene bleiben bis dahin offen. Sprachverständnis,
Einwandwirkung, Audio und reale Telefonie werden nicht durch Offline-Fakes ersetzt.

## 7. SDK-Entscheidung und ausführbarer Folgeauftrag

**Vorgeschlagene Basis für P1: vorhandenes Original mit LiveKit Agents 1.8.0
und unverändertem `uv.lock`. Kein Upgrade oder Downgrade Teil des Pakets.**
Heute importiert: Python 3.13.13, `livekit-agents` 1.8.0; Lockfile ebenfalls 1.8.0.
Manifest erlaubt `>=1.8.0,<2`, daher für Wiederholungen den Lockstand verwenden.
Kein Nachweis über den aktuell laufenden Cloudagenten und keine Behauptung,
1.8.0 sei die heute neueste verfügbare Releaseversion.

Aktuell über den offiziellen LiveKit-Docs-MCP gelesen:
[Workflows](https://docs.livekit.io/agents/logic/workflows.md),
[Tests](https://docs.livekit.io/agents/start/testing.md),
[Sessions](https://docs.livekit.io/agents/logic/sessions.md).
Tasks/TaskGroup und call-lokales `userdata` passen zum gezielten Delta. Offizielle
Text-Verhaltenstests nutzen ein LLM; ohne Raumverbindung heißt nicht providerfrei.
Das lokale Paket verwendet deshalb bestehende deterministische Fakes und
gemockten Jobkontext. Keine neue Testplattform oder Cloudverbindung erforderlich.

Frisch lokal kontrollierte API-Punkte: `TaskGroup` besitzt
`on_task_completed`, `summarize_chat_ctx=True`, `return_exceptions=False`;
`AgentTask.complete(self, result)` ist synchron; `AgentSession.shutdown(self, *,
drain=True)` ist synchron; `RunContext.disallow_interruptions(self)` vorhanden.
Task-Completion-Callback ergänzt vollständige Taskresultate, ersetzt aber nicht
die Erhaltung von Werten während einer unvollendeten Aufnahme. SDK-Schutz ersetzt
keine Backendtransaktion. Keine neue API aus Erinnerung vorausgesetzt.

### Freigabegegenstand: lokal formulierter Umsetzungsauftrag

> Implementiere ausschließlich P1a dieses Berichts im Originalprojekt
> `/Users/activi/Documents/ChatGPT/Livekit agent` auf dem frisch gesicherten
> tatsächlichen Arbeitsbaum. Trenne Gesprächserlaubnis, geäußertes Interesse,
> Rückrufzustimmung und tatsächlichen Abschluss. Behebe die beiden dokumentierten
> Repros einschließlich ihrer Task-/State-Ursachen. Erhalte bestätigte Teilangaben,
> vorhandene Buchungsbelege und unbekannte Operationsausgänge beim Ende.
> Führe P1-01–P1-15 innerhalb der vorhandenen deterministischen pytest-Infrastruktur
> aus und kennzeichne Fake-Vertragsannahmen ausdrücklich. Belasse SDK und Lockstand
> auf der geprüften Originalbasis. Neue Ergebnisformen dürfen den realen
> N8nEnergyBackend ohne angenommene Empfängerrevision nicht erreichen.
> Berichte separat über lokale Erfüllung, offene AC-Anteile und P1b-Vertragsgates.
> Keine externe Aktion, kein Commit/Push/Deployment ohne eigenen Auftrag.

Dieser Block ist ein **Freigabevorschlag**, keine bereits erteilte Erlaubnis.
Vor Beginn braucht es eine konkrete lokale Implementierungsfreigabe für P1a
einschließlich der bezeichneten R-/AC-Teilmenge und Schutzdeltas. Sie kann als
begrenzte Teilfreigabe erfolgen, ohne SV01–SV08 oder die ganze Produktabnahme
vorwegzunehmen. Gesamtfachabnahme bleibt ein eigener Entscheid.

Erlaubte Änderungsstellen nach dieser Freigabe: die in Abschnitt 4 benannten
Agent-/State-/Resultgrenzen, erforderliche Fake-/Adaptertrennung in
`src/michaela/backend.py`, die betroffenen vorhandenen Testmodule und bei
geänderter Phasenbeschreibung gezielt `src/michaela/plan.py`. Keine allgemeine
Tarif-/Spartenneuentwicklung, Umbuchung, Kalenderfallback, Telefonietreiber,
Providerkonfiguration oder Neuerfassung fremder Personen.

Für ticketausgeführte Arbeit zusätzlich: konkrete Zuordnung mit richtigem Root,
bereinigte ADR-006-Policy und erfüllte native Blocker. ACT-42 ist der naheliegende
fachliche Anknüpfungspunkt für Export, ACT-43 für Operations-/Bindungsanteile;
dieser Bericht weist keinem Ticket neue Inhalte zu und teilt es nicht selbst.
Ein gesondertes enges Offline-Ticket kann nur im vorgesehenen Supervisorprozess
zugeordnet werden. P1b benötigt zusätzlich die Vertragsannahmen aus Abschnitt 3
und deren Empfängernachweis. Heute ist kein solches ausführbares Ticket belegt.

### Rückweg

Vor späterem Edit aktuellen Branch, HEAD, Index, untracked Test und Prüfsummen
erneut erfassen; gezielt betroffene vorhandene Dateien sicher erhalten. Bei Drift
den Delta-Scope neu vergleichen, keine fremden Änderungen zurücksetzen.
P1a lokal nur über die eigenen geprüften Hunks zurücknehmen, niemals über
pauschales `git reset`/Ordnersynchronisation. Keine Commitannahme aus HEAD.
Vor P1b Rückwärtslesbarkeit und Revisionen vereinbaren: Rollback des Senders
löscht weder Buchung noch Sperre, bestätigte Kundenrevision oder offene Operation.
Wenn der alte Sender neue Zustände nicht verlustfrei darstellen kann, keinen
verlusthaften Legacy-Fallback aktivieren; betroffene neue Ausführung bis zur
verträglichen Version stoppen. Dauerhaft offene Vorgänge bleiben beim vereinbarten
Owner unter ihrer ursprünglichen Operationsreferenz klärbar.

## 8. Tatsächlich ausgeführte Offline-Prüfung

Zeit: **09.09.2026 22:44:36–22:44:40 UTC**, entsprechend **10.09.2026
00:44:36–00:44:40 Europe/Sarajevo**. Ausschließlich Original, vorhandene uv-Umgebung,
`uv run --no-sync --offline`. Keine Synchronisierung oder Installation.
Umgebung auf PATH/HOME/LANG reduziert; Bytecode, pytest-Cache, automatische
pytest-Plugins und Ruff-Cache deaktiviert; temporärer uv-/pytest-Pfad.
Vorhandener `offline_guard.py` blockiert Socket-Verbindungen und `.env`-Laden;
er wurde vor pytest/Produktimports geladen. `pytest_asyncio.plugin` explizit aktiviert.
Tests/Fakes vor Ausführung gelesen; keine Provider-/n8n-Ausführung.

| Prüfung | Ergebnis |
|---|---|
| Vorhandene Suite `tests` | **PASS: 79 passed in 1.05s**, Exit 0. |
| Ruff `src tests` | **PASS**, Exit 0. |
| Ruff Format `src tests` | **PASS: 19 files already formatted**, Exit 0. |
| Ruff gesamtes Repo | **FAIL**, Exit 1: I001 und UP017 in `docs/audits/reconciliation/2026-09-05T220358Z/VERIFY_LOCAL.py`. |
| Ruff Format gesamtes Repo | **FAIL**, Exit 1: dieselbe Datei; 1 würde formatiert, 192 bereits formatiert. Historisches Audit unverändert. |
| Bestehender Repro | Beide Fehler erneut beobachtet; keine Behebung. |
| SDK-/Lockprüfung | **PASS**, beide 1.8.0; lokale API-Punkte oben. |
| Mypy | Nicht ausgeführt; im aktuellen Projektmanifest weder als Tool noch als Prüfung konfiguriert. |
| Paketbuild | Nicht ausgeführt; keine Packagingänderung dieses Reviews. Bei späterer Packagingänderung `uv build` erforderlich. |
| Provider/Cloud/SIP/n8n/E2E | Nicht ausgeführt; ausdrücklich außerhalb des Auftrags. |

Vor/nach dem Prüflauf: **319 erfasste bestehende Quellen, Manifeste und
Dokument-/Evidenzdateien bytegleich**, davon 28 Dateien in src/tests/scripts/
simulations. Keine Aussage über ignorierte Runtime-/Cachedateien oder einen
insgesamt sauberen Git-Arbeitsbaum. Der abschließende Abgleich prüft diese
erfassten Dateien erneut und die neuen Berichtverweise separat.

### Reproduktion im Original ohne historische Nachweise zu überschreiben

Das historische `verify_baseline.py` wird hier nicht gestartet, weil es auch
den ausgeschlossenen zweiten Arbeitsbereich prüft. Folgender Aufruf wiederholt
ausschließlich vorhandene Originaltests und den vorhandenen Minimal-Repro;
Cache-/Arbeitsdateien gehen in ein temporäres Verzeichnis:

```bash
rtk proxy bash <<'BASH'
set -euo pipefail
review_root='/Users/activi/Documents/ChatGPT/Livekit agent'
review_tmp=$(mktemp -d /tmp/michaela-original-review.XXXXXX)
cd "$review_root"
export PYTHONDONTWRITEBYTECODE=1
review_pythonpath="$review_root/docs/coordination/energywarm/reports/20260909-agent-comparison-evidence:$review_root:$review_root/src"
env -i PATH="$PATH" HOME="$HOME" LANG="${LANG:-C}" \
  PYTHONDONTWRITEBYTECODE=1 PYTEST_DISABLE_PLUGIN_AUTOLOAD=1 \
  UV_CACHE_DIR="$review_tmp/uv" PYTHONPATH="$review_pythonpath" \
  rtk proxy uv run --no-sync --offline python -c \
  'import offline_guard, pytest; raise SystemExit(pytest.main(["-p", "pytest_asyncio.plugin", "-p", "no:cacheprovider", "-q", "tests"]))'
env -i PATH="$PATH" HOME="$HOME" LANG="${LANG:-C}" \
  PYTHONDONTWRITEBYTECODE=1 UV_CACHE_DIR="$review_tmp/uv" \
  PYTHONPATH="$review_pythonpath" \
  rtk proxy uv run --no-sync --offline python \
  docs/coordination/energywarm/reports/20260909-agent-comparison-evidence/repro.py
BASH
```

Das ist ein Wiederausführungsbeispiel, keine neu eingeführte Testplattform.
Repositoryweite Lintbefunde bleiben eine bekannte unabhängige Einschränkung;
keine Reparatur historischer Nachweise aus diesem Vorbereitungsauftrag ableiten.

## 9. Abnahmeentscheidung, die jetzt prüfbar vorliegt

Der Auftraggeber kann den Outbound-Sollablauf R01–R21/M01–M44/AC01–AC46 mit den
Präzisierungen aus Abschnitt 2 zur fachlichen Grundlage erklären; AC47/R22
bleiben für diesen direkten Originalumfang ausgenommen und durch die lokale
Basis-/Prüf-/Rückwegauflage ersetzt. Das ist keine Aussage über bestandene
Produkttests oder gemeinsame API-Annahme. Die zehn Einzelentscheidungen sind
bereits bestätigt und bleiben unverändert.

Für den nächsten lokalen Arbeitsschritt fehlt die konkrete **P1a-Freigabe im
Original**. Für den wirklichen vollständigen Ergebnisexport fehlen zusätzlich
**angenommene Ergebnis-, Bindungs-, Quittungs-/Recovery- und Lifecycleverträge,
passende Empfängerunterstützung und im Workerprozess eine gültige Ticketzuordnung**.
Der Bericht ist damit eine konkrete Review- und Freigabegrundlage, kein
Implementierungs- oder Produktionsfreigabenachweis.

## 10. Prüfsummen der bewerteten Basis

SHA-256, Arbeitsdateien im Original während des oben bezeichneten Prüflaufs.
Die Berichtdatei selbst gehört nicht zur vorher erfassten Schutzbasis.

| Datei relativ zum Original | SHA-256 |
|---|---|
| `src/agent.py` | `6cda0192f74bfe4e2c152cbc2d13e751974e1286578d8817d12fcf46f7efe28f` |
| `src/michaela/state.py` | `b189eae10cb287ec571e4bd97a6cd4bfec9307e06289e2f1eb624ae30c5ca8fc` |
| `src/michaela/backend.py` | `afb5cfa81d052fe7a679caf58442fd0237d07d1adbefbf016e5263569a904f4a` |
| `src/michaela/result.py` | `ee139a8f425e12d5ee5a505dd72cab51bfc32ab2d3b50b0eb8f8cf14a444bdb8` |
| `pyproject.toml` | `6c2f5c801bbd8e3af9861d3d9f6098026e5c5bd85f8403ebb052d5a03e00d55f` |
| `uv.lock` | `85149eef5b4df65c1609fd58537d22199f91574ebfc1df02ca2c3062816468f8` |
| `tests/test_agent_logic.py` | `861e1a55e28ad86e465dc5e4ae003f338a34349091b9f19d4513fda33d4914fc` |
| `tests/test_connectivity_regressions.py` | `8551cf25187b874836981f139d143c32f44cfc0cb8bb996752ede2fac5599b68` |
| `docs/coordination/energywarm/reports/20260909-michaela-spezifikation.md` | `6d8038da04385e4c557f4fc32ad76caeae830af29d03c03fad079ead49b34c05` |
| `docs/coordination/energywarm/reports/20260909-michaela-spec-matrix.md` | `9152a8914cf99c01a0c4be236ff39a509d392a3aefaf6b51c6b0c92142b2af2a` |
| `docs/coordination/energywarm/reports/20260909-michaela-spec-vertraege.md` | `48b40c986b6108eef052c139520768db803ac2b4052bc81168e63e8ad2673335` |
| `docs/coordination/energywarm/reports/20260909-michaela-spec-nachweis.md` | `39e2ac2629b39b37ff658556f4423a343c6fe05a609c913e2d10c3cc05874cbf` |
| `docs/coordination/energywarm/reports/20260909-michaela-sollablauf-workshop.md` | `2e26e13e9dee1692f2723bf94dda387a9b5b2e210be9373ade7d7bbdfe3ec09b` |
| `docs/coordination/energywarm/reports/20260909-michaela-leadstatus-zur-abnahme.md` | `af9118dc0ca2016271d30eb7362f3192f7410c2010ab2bef32e5498445fea395` |

Abschließender lokaler Abgleich: 319 erfasste vorhandene Dateien unverändert;
alle 10 lokalen Berichtverweise auf vorhandene Ziele aufgelöst; keine
nachgestellten Leerzeichen. Strukturzählung: 22 Anforderungen, 44 Matrixpfade,
47 Abnahmekriterien, acht Vertragsvorschläge jeweils ohne fehlende oder doppelte
Definition. Diese Kontrollen sind Dokumentationsnachweise, keine Produktabnahme.
