# Michaela: Quellprüfung und Nachweise zur Spezifikation

Teil der [Spezifikation](20260909-michaela-spezifikation.md). **PASS_WITH_GAPS**
für Dokumentation und aktuellen Offline-Bestand. Keine Produktimplementierung,
keine fachliche Gesamtabnahme und keine Produktionsfreigabe.

Direkter Nutzerauftrag, Task `01a08828-f991-71a1-b062-c679b4f75672`, tatsächliche
Koordinationswurzel `/Users/activi/Documents/ChatGPT/Livekit agent`.
Keine registrierte Workerrolle, kein Linear-Claim und kein externer Write.
Zeiten sind UTC; die Sitzung reicht lokal in den 10.09.2026 hinein.

## Tatsächlicher Ausgangsstand

| Merkmal | Original | Simulation V3 |
|---|---|---|
| Geprüfter Pfad | `/Users/activi/Documents/ChatGPT/Livekit agent` | `/Users/activi/Documents/ChatGPT/Livekit agent Simulation V3` |
| Git HEAD, frisch via globalem Git-MCP gelesen | `99de8d766f6af275a04c7c8eae652a801b8a366b` | `43dc9d443d131b0735fd3786ccf9896665e26742` |
| Arbeitsbaum | Bereits verändert, unter anderem Agent/State/Backend/Manifeste/Tests und zahlreiche Dokumente | Bereits verändert, zusätzliche Simulations-/Telefoniequellen und Tests |
| Agents SDK lokal importiert | 1.8.0 | 1.7.1 |
| `uv.lock`: livekit-agents | 1.8.0 | 1.7.1 |
| `src/agent.py` SHA-256 | `6cda0192f74bfe4e2c152cbc2d13e751974e1286578d8817d12fcf46f7efe28f` | `e01a76290ace4fd98a9e2a857ab39dfcce8cfcdea22db43119031c0fabeb7555` |
| Strukturell verglichene Task-Klassen | 16: 15 konkrete Tasks und Basisklasse | Dieselben 16, AST ohne Positionsattribute identisch |
| Geschütztes Inventar im Prüflauf | 27 Quell-/Test-/Simulations-/Script-/Manifest-/AGENTS-Dateien | 152 entsprechende Dateien |

Die Arbeitsdateien, nicht nur HEAD, sind die Bewertungsbasis. Vor und nach den
Prüfungen waren alle erfassten 27/152 Dateien bytegleich. Ein insgesamt sauberer
oder vollständig unveränderter Arbeitsbaum wird nicht behauptet. Neue lokale
Spezifikations-/Evidenzdateien sind beabsichtigt; bestehende Produkt- und
Auditdateien wurden nicht geändert.

Historische Hinweise wurden gelesen, nicht als frische Beweise übernommen:
[Quellvergleich](20260909-michaela-vs-v3.md),
[Dokumentenvergleich](20260909-agent-comparison-documented.md),
[Workshopnachweise](20260909-michaela-sollablauf-evidence/source-and-tests.json)
und [dessen Abschlussabgleich](20260909-michaela-sollablauf-evidence/final-documentation-check.json).
Der ältere Quellvergleich beschreibt noch bytegleiche Dependency-Manifeste;
das ist durch die heutige Originalaktualisierung auf 1.8.0 überholt. Die hier
frisch gelesenen Manifeste und tatsächlichen Imports entscheiden.

## Frische Prüfungen und Ausführungsgrenzen

Prüflauf 09.09.2026 **21:56:36–21:56:42 UTC**, korrigierte Repro-/Lint-Prüfung
**21:57:44–21:57:47 UTC**. Ausführung über vorhandene uv-Umgebungen mit
`--no-sync --offline`, deaktiviertem Bytecode-/pytest-/Ruff-Cache, temporären
Test-/uv-Verzeichnissen und kontrollierter Umgebung. Der vorhandene
[Offline-Guard](20260909-agent-comparison-evidence/offline_guard.py) blockiert
Python-Socket-Verbindungen und `.env`-Laden. Testquellen wurden auf bestehende
Fakes/Mocks und Providerisolation geprüft. Keine Modell-, Kalender-, n8n-,
Cloud- oder Telefonieaufrufe wurden ausgeführt.

| Prüfung | Original | V3 | Bedeutung |
|---|---|---|---|
| Bestehende pytest-Suite | 79 PASS, 0 Fehler/Failures/Skips | 132 PASS, 0 Fehler/Failures/Skips | Bestehende deterministische Tests; neue AC nicht dadurch bestanden. |
| Ruff Produktbereiche | PASS: `src tests` | PASS: `src tests scripts/simulations` | Aktueller Produkt-/Testcode lokal lintfrei im geprüften Umfang. |
| Format Produktbereiche | PASS | PASS | Keine Produktformatierung geändert. |
| Ruff gesamtes Repo, korrigierter Nachlauf | FAIL: zwei historische Befunde | FAIL: dieselben zwei | I001/UP017 in `docs/audits/reconciliation/2026-09-05T220358Z/VERIFY_LOCAL.py`. |
| Format gesamtes Repo, korrigierter Nachlauf | FAIL: dieselbe historische Datei | FAIL: dieselbe historische Datei | Unveränderte historische Auditdatei; außerhalb des Spec-Auftrags. |
| Vorhandene zwei Minimal-Repros | Beobachtete Fehler reproduziert | Dieselben Fehler reproduziert | Tool-/State-Nachweis, kein echter Kundendialog. |
| SDK-Signaturen | Geprüft | Geprüft | betrachtete Signaturen gleich; kein Beweis gleicher SDK-Semantik. |
| Mypy | Nicht ausgeführt | Nicht ausgeführt | Nicht in den gelesenen Projektmanifesten als Tool/Prüfung konfiguriert. |
| Paketbuild | Nicht ausgeführt | Nicht ausgeführt | Keine Packaging-/Produktänderung dieser Sitzung. |
| Provider-/Audio-/SIP-/n8n-/E2E | Nicht ausgeführt | Nicht ausgeführt | Vom Auftrag ausgeschlossen; kein Erfolg behauptet. |

Belege:
[vollständiges Baselineinventar](20260909-michaela-spec-evidence/baseline.json),
[korrigierte Prüfungen](20260909-michaela-spec-evidence/corrected-checks.json),
[Original-JUnit](20260909-michaela-spec-evidence/original-tests.xml),
[V3-JUnit](20260909-michaela-spec-evidence/v3-tests.xml),
[Original-SDK](20260909-michaela-spec-evidence/original-sdk.txt),
[V3-SDK](20260909-michaela-spec-evidence/v3-sdk.txt),
[Original-Repro](20260909-michaela-spec-evidence/corrected-checks-original-repro.txt),
[V3-Repro](20260909-michaela-spec-evidence/corrected-checks-v3-repro.txt).

Der erste Repro-Aufruf scheiterte wegen fehlendem Repo-Root im Prüf-PYTHONPATH,
nicht wegen eines Produktimports. Der Prüfpfad wurde berichtigt und nur Repro/
Lint/Format erneut ausgeführt; die bestandenen Produkttests wurden nicht unnötig
wiederholt. Das neue Evidenzscript hatte anfänglich eigene Stilbefunde; diese
wurden nur in dieser neuen Datei korrigiert. Die korrigierten Repo-Prüfungen
zeigen ausschließlich die zwei historischen Befunde. Die ursprünglichen
Logs bleiben für Nachvollziehbarkeit erhalten. Ein direkter uv-Aufruf ohne
temporären Cache scheiterte am Sandboxzugriff auf den globalen Cache; der
zulässige temporäre Cache löste dies ohne Eskalation oder globale Änderung.

Reproduzierbarer Bestandsprüfer:

```bash
rtk proxy python3 docs/coordination/energywarm/reports/20260909-michaela-spec-evidence/verify_baseline.py
```

Dies ist ein lokales Evidenzscript, keine neue Testplattform. Es führt bestehende
Tests/Prüfungen aus und schreibt ausschließlich eigene Nachweise; Standardlauf
erneuert seine Baselineartefakte. Für einen gesonderten Nachlauf `--run-name`
verwenden, zum Beispiel `--checks ruff format repro --run-name corrected-checks`.
Kein Scriptaufruf erteilt neue Produkt- oder Providerfreigaben.

## Frisch bestätigte Befunde

| ID / Art | Beobachtung und Nachweis | Spezifikationsfolge |
|---|---|---|
| F01 / ausgeführter Repro + Serena | `_pack_dc_results` liefert bei `permission=False` ohne anderen Wunsch `outcome_norm=interessiert` und `termin_art=ai`. PermissionTask kündigt bei negativem Ergebnis pauschal einen Rückruf an. | R02/R09, AC03/04: Erlaubnis, Zeitmangel, Interesse und Rückrufzustimmung trennen. Keine tatsächlich ausgeführte ungewollte Buchung behauptet. |
| F02 / ausgeführter Repro + Serena | `build_final_payload` für falsche Person scheitert mit `final result requires an explicit outcome`; validate_final koppelt Interesse/Termin an Buchung. | R18, AC40: vollständige terminale Matrix unabhängig vom Verkaufsoutcome. |
| F03 / statisch direkt gelesen | KwhPreisTask.on_enter überspringt den Preis bei beliebigem truthy Jahresverbrauch. Ein bekannter Verbrauch verhindert damit die verlangte Preisfrage. | R05, AC12; gezielter späterer Verhaltenstest. |
| F04 / ausgeführter Helper-Repro + Serena | `_booking_explicitly_confirmed('Jahresverbrauch')` ergibt True wegen Teilstring `ja`. Der Helper prüft keinen konkreten Angebotsbezug. | R10, AC20: konkrete Bestätigung statt Teilstring. Helper-Repro beweist keine reale LLM-Buchung. |
| F05 / ausgeführter State-Repro + Serena | CallState.validate_booking akzeptiert einen angebotenen Human-Slot bei explizitem Bool True trotz identity=False, permission=False und Abbruchmarker; diese Schranken fehlen auf dieser Grenze. | R03/R04/R10, AC07/21: Fachschranken zusätzlich zu Slotprüfung. Keine externe Buchung ausgeführt. |
| F06 / statisch direkt gelesen | Einzelne Tarif-/Kontaktrevisionen liegen nicht vollständig im CallState; beim TaskGroup-Abbruch werden nur Identitätsresultate und begrenzter öffentlicher State gepackt. | R14/R16/R18: bestätigte Werte bei Aufnahme erhalten, Abbruch ohne Taskabschluss prüfen. |
| F07 / statisch direkt gelesen | Buchungstool validiert positiven Beleg, speichert im State aber nur Slot/Art/abgeleitete Zeiten; kein dauerhafter unbekannter Operationszustand oder Statusklärungsweg. | R13/R19; SV03/SV05. |
| F08 / statisch direkt gelesen | `save_result` liefert HTTP-Body, `export_final_result` prüft ihn fachlich nicht; `_on_session_end` markiert bei fehlender Ausnahme Erfolg und loggt Fehler ohne belegten dauerhaften Recoveryweg. | R18/R19; Speicherquittung, Wiederherstellung und keine HTTP-200-Erfolgsannahme. |
| I01 / statisch direkt gelesen | Bindung aus Metadaten, angebotener Slot und Art werden geprüft, negativer/unvollständiger Buchungsbeleg abgewiesen, alte Angebote bei Fehler/Wechsel entwertet. | Bestehende Schutzmechanismen erhalten, nicht ersetzen oder als vollständig ausreichend ausgeben. |
| I02 / frisch strukturell verglichen | Dieselben 16 Taskkörper in Original/V3. Zusätzliche V3-Tests/Runtime machen keine automatisch bessere Gesprächsführung. | Einzelne Aufgaben nach Zweck bewerten. |
| I03 / vorhandene Schnittstelle | Nur Kunde, Slots, Buchung, Ergebnis in EnergyBackend. Keine Methoden für sichere Umbuchung, Datenupdate, Human-Übergabe, Auftrag ohne Slot oder Statusklärung. | SV02–SV07 sind Integrationsanforderungen und keine vorhandenen Fähigkeiten. |

Die Zusatzprobes F04/F05 wurden im Original mit geladenem Offline-Guard und
synthetischer Callbindung ausgeführt. Tatsächliche Ausgaben: `True` und `human`.
Die identischen geprüften Task-/State-Prüfungen in V3 liefern statisch dieselbe
Schrankenlücke; kein zusätzlicher dortiger Ausführungslauf wird behauptet.
Der Statusmarker im State-Repro ist nur synthetischer Testzustand, kein neues
implementiertes Kontaktstoppfeld.

## Einzelbewertung aller 16 Task-Klassen

Alle Task-Symbole liegen heute in [src/agent.py](../../../../src/agent.py).
Die empfohlenen Änderungen sind V-Vorschläge innerhalb der R-Anforderungen;
die Zahl der Klassen bestimmt keinen Umbau.

| Task | Frisch verifizierter Istbezug | Gezielte Umsetzungsvorbereitung | R / AC |
|---|---|---|---|
| MichaelaFieldTask | Baut eigene Instruktionen und Skip-/Rückrufzweige; Hauptprompt wird nicht einfach mitverwendet. | Gemeinsame Gesprächsregeln und aktueller Fachzustand verfügbar; Skip nach tatsächlichem Ende/Wunsch statt negativer Permission. Basis weiterhin sinnvoll. | R01/02/16; AC02/03/36 |
| IdentitaetTask | Unterschied `nicht_da`/`verwaehlt`, danach unmittelbares Ende; keine strukturierte Erreichbarkeitshinweis-/Neupersonbindung. | Identitätsziel behalten; Haushaltsauskunft/Übergabe/eigene Beratung mit vollständigem Abschluss und Bindung. | R04; AC08–AC10 |
| PermissionTask | Bool plus History-Heuristik; negative Erlaubnis mit Rückrufansage. | Eigene Situationsklärung sinnvoll; Erlaubnis, Zeitmangel, Einwand und expliziten Folgewunsch differenzieren. | R02/03; AC03–AC07 |
| PainTask | Antwort-/History-Heuristiken; Bedarf wird über einzelne Wörter beurteilt. | Bedarf optional passend verstehen; keine erzwungene Unzufriedenheit oder Preisersparnis. Nicht als Human-Freigabeschranke verwenden. | R03/08; AC05/06/16 |
| EnergieartTask | Ein `wert`, ergänzende History-Ableitung. | Aktuelle bestätigte gewünschte Sparten als Fachzustand; Gas-only, spätere Gasergänzung und Entfernen einer Sparte prüfen. | R05/16; AC11/13/36 |
| AktuellerVersorgerTask | Liste lokaler Teilresultate; Abschluss liefert Liste. | Eindeutiger aktiver Anbieter je Sparte mit bestätigter Revision; kein Duplikat statt Korrektur, kein Human-Pflichtfeld. | R05/14/16; AC11/18/35 |
| JahresverbrauchTask | Ein String `kwh`; zusätzlich einzelnes Flowfeld. | Pro Sparte Wert/Einheit/Qualität erhalten, fehlend von Zahl unterscheiden. Mehrfeldaufnahme möglich, kein eigenständiger Slotnachweis. | R05/07; AC11/12/15 |
| JahresgrundpreisTask | Ein String `euro`, nur Taskresultat. | Pro Sparte Bezugszeit erhalten; deterministisch umrechnen nur bei eindeutigem Bezug; Teilstand vor Taskende sichern. | R05/16/18; AC11/35/40 |
| KwhPreisTask | `on_enter` beendet ohne Preis bei vorhandenem Verbrauch. | Diese konkrete Skipregel korrigieren; Preis je gewünschter Sparte aktiv erfassen. Kein Grund für Komplettumbau anderer Tasks. | R05; AC12 |
| ZaehlernummerTask | Einzelner optionaler String im Taskresultat. | Je Sparte aktiv erfragen, bei fehlend/verweigert offenlassen; keine Human-Buchungsschranke. | R05/06/08; AC11/14/18 |
| OutcomeTask | Schreibt beschränktes Outcome; generische Tasks erhalten keine Kalenderwerkzeuge. | Tatsächlichen Wunsch/Endgrund ableiten; keine bereits erfolgreiche Buchung aus einer Aufforderung oder Permission. Prompt-/Toolreichweite kohärent machen. | R02/08/18; AC03/16/40 |
| NeinArtTask | Liefert `nein_art` als Taskresultat; keine eigenständige sofortige Stoppschranke. | Ende/Stoppsignale phasenübergreifend wirksam; keine automatische Vertagung durch „weich“. Eigener Dialog nur bei echtem Klärungsbedarf. | R03; AC05/07 |
| GrundTask | Freitextresultat; Rückruflogik kann Grund vorgeben. | Nur tatsächlich genannten Grund erhalten; Kunde muss keine weitere Rechtfertigung liefern. | R02/03/18; AC03/07/40 |
| TerminArtTask | Schreibt Art aus Erfassung/Outcome-Zweig, Rückruflogik automatisch AI. | Wunschart und tatsächliche Buchung trennen; Human-Regel und explizite AI-Zustimmung anwenden. | R08/09; AC16–AC19 |
| TerminStartTask | Erhält die Kalender-/Buchungstools; record übernimmt nur den gebuchten State-Start. | Eigenständige Terminphase sinnvoll; Angebot/Zustimmung/Beleg/Fehlerzustände präzisieren, echte Zeitpräferenz nicht als Buchung behandeln. | R10–R13; AC20–AC29 |
| TerminEndeTask | Gibt bereits im State vorhandene Anfangs-/Endzeit zurück. | V: deterministischen Ergebniswert ohne eigenen LLM-Dialog verwenden, sofern Vertrag Dauer/kanonische Zeit klärt. | R10/22; AC23/47 |

## Implementierungs- und Testlandkarte

| Grenze | Verifizierte Symbole / Dateien | Relevante Entscheidung |
|---|---|---|
| Gespräch/Orchestrierung | [agent.py](../../../../src/agent.py): DefaultAgent.on_enter, `_finish_data_collection`, `_pack_dc_results`, `_booking_explicitly_confirmed`, `_on_session_end` | Fachliche Zwischenstände und vollständiger Abschluss; Tools nach Phase; keine History als kanonische Datenbank. |
| Fachzustand | [state.py](../../../../src/michaela/state.py): CallState, offer_slots, validate_booking, confirm_booking, validate_final | Orthogonale Dimensionen, aktuelle Revision und belegte Buchung; bisherige Bindungs-/Slotinvarianten erhalten. |
| Backend | [backend.py](../../../../src/michaela/backend.py): EnergyBackend, N8nEnergyBackend, validate_booking_response | Zentraler Adapter bleibt einzige Grenze; neue Fähigkeiten erst nach angenommenem SV-Vertrag. |
| Ergebnis | [result.py](../../../../src/michaela/result.py): build_final_payload, export_final_result | Alle terminalen Fälle, Quittung und korrelierte spätere Klärung. |
| Diagnose | [events.py](../../../../src/michaela/events.py): EventJournal | Call-lokal und redigiert; nicht als dauerhafter PII-Recoverystore zweckentfremden. |
| Feldplan | [plan.py](../../../../src/michaela/plan.py): CollectionPlan | Aufgabenreihenfolge/Tools; keine pauschale neue Taskarchitektur. |
| Offline-Grenze | [conversation_harness.py](../../../../tests/conversation_harness.py): ConversationHarness.offer/book/finish | Prüft State/Fake/Export, aber setzt Outcome/State selbst; keine Spracheingabe. |
| Agent-/Schrankenregression | [test_agent_logic.py](../../../../tests/test_agent_logic.py), [test_state.py](../../../../tests/test_state.py), [test_plan.py](../../../../tests/test_plan.py) | Aufrufen echter Record-/Toolpfade ergänzen; überholte Zeitmangel-Erwartung gezielt korrigieren. |
| Backend-/Lifecyclefehler | [test_connectivity_regressions.py](../../../../tests/test_connectivity_regressions.py), [test_backend_validation.py](../../../../tests/test_backend_validation.py), [test_result.py](../../../../tests/test_result.py), [test_events.py](../../../../tests/test_events.py) | Vorhandene negative Quittungen, Slotentwertung und Sessionreport-Fälle erweitern; keine unerlaubten echten Provider. |
| V3-Laufzeit | [simulation.py](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/src/michaela/simulation.py>) und [Runtime-Tests](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/tests/test_simulation_runtime.py>) | Vorhandene ScenarioBackend-Faults und Ergebnisbewertung nutzen; direkt gesetzte Kontaktwerte sind kein Erfassungsnachweis. |
| V3-Telefonieprototyp | [call_control.py](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/src/michaela/call_control.py>) und [Tests](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/tests/test_call_control.py>) | Lokaler Testtransport, kein produktiver Call-Controller-/n8n-Ersatz. |

Die V3-ADRs zu [Kontakt/Gas](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/docs/decisions/2026-09-06-simulation-contact-and-gas.md>),
[anderer Person](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/docs/decisions/2026-09-06-wrong-person-routing.md>),
[Providerfehlern](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/docs/decisions/2026-09-06-provider-failure-policy.md>),
[Telefonie](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/docs/decisions/2026-09-06-telephony-outcomes.md>)
und [n8n-Ownership](</Users/activi/Documents/ChatGPT/Livekit agent Simulation V3/docs/decisions/2026-09-06-n8n-retry-ownership.md>)
wurden gelesen. Sie begründen Fach- und Vorbereitungserwartungen mit ihrem
jeweiligen Scope, keine neuen produktiven Wirewerte.

## Dokumentations-/Zugriffsprüfung und Arbeitsbericht

| Phase / Schritt | Absicht und Aktion | Tatsächliches Ergebnis / Grenze |
|---|---|---|
| M0, Sitzungseinstieg | Anfrage, geltende AGENTS/Overrides und MCP-Routing lesen; Serena-Handbuch und Originalaktivierung. | Original aktiv; vorhandene Memories angezeigt, kein Onboarding. |
| M0, Kontext | Hivemind rules/goal read; lokaler read-only Fallback. | Nicht angemeldet; lokaler Index fehlt. Projekt-/ADR-/Sitzungsquellen verwendet, kein Login/Memorywrite. |
| M0, Skills | `/to-spec` in `.agents/skills/to-spec/SKILL.md` gefunden und gelesen; livekit-agents angewendet. | Synthese ohne erneute Fachfragen. Direkter Auftrag übersteuert Ticketveröffentlichung und zusätzliche Testgrenzen-Rückfrage. |
| M0, gemeinsame Grenzen | PROJECTS.json, Worker-Routine, ADR-005, gemeinsame Domain/Entscheidungs-/Vertrags-/Abnahmedokumente lesen. | Keine Rollenübernahme/Queue-Auswahl. ADR-006-Hinweise und V3-Grenzen berücksichtigt. |
| M0, Zugriff | Bestehende reine Dateizugriffsprobe mit `--setup-session`. | [PASS für Dateizugriff](20260909T215652492708Z-access.json), ausdrücklich kein Workerclaim oder Providerzugriff. |
| M1, Quellen | Serena-Symbolübersicht und gezielte Methoden; AST-/SHA-Vergleich beider Roots; globale Git-Status-/Logreads. | Arbeitsstände, Taskgleichheit und konkrete Fehler belegt; Nutzeränderungen erhalten. |
| M1, offizielle Dokumentation | Vorhandener LiveKit-Docs-MCP: Tasks, Handoffs, Tools, Tests, Sessions; bei abgeschnittenem Output gezielte Tool-/Testauszüge. | Aktuelle offizielle Konzepte, lokale SDK-Signaturen gegengeprüft. Keine Quellcodesignatur aus Erinnerung geraten. |
| M2, Offline-Nachweis | Bestehende Tests, Ruff/Format, Repros und SDK-Imports mit Offline-Guard. | Ergebnisse wie oben; keine Produktreparatur, historische Lintbefunde erhalten. |
| M2, Spezifikation | Hauptdokument, Fallmatrix und acht Supervisor-Vertragsvorschläge anlegen. | Fachliche Entscheidungen, Iststand, Fehler, Umsetzungsvorschläge und Gates getrennt. |
| M4, Abschlussprüfung | Neue Markdownverweise, stabile R/AC/M/SV-IDs, Quellschutz und neue Evidenzdatei prüfen. | [Abschlussvalidierung](20260909-michaela-spec-evidence/final-validation.json); kein AC-Erfüllungsclaim für das Produkt. |

Keine externen Ziele wurden geändert. Erlaubter Umfang war die angeforderte
lokale Spezifikation und read-only/offline Verifikation. Vollständige neue
Spezifikation ist reviewbar; tatsächliche Implementierung und gemeinsame
Vertragsannahme stehen aus. Nächste Aktion ist U0/U1 aus dem Hauptdokument,
anschließend enges freigegebenes V3-Paket, keine automatische Originalübernahme.
