# Michaela: Schnittstellenanforderungen zur Supervisorprüfung

Stand: 09.09.2026 UTC. **SV01–SV08 SIND VORSCHLÄGE, KEINE ANGENOMMENE
VERTRAGSREVISION.** Teil der [Spezifikation](20260909-michaela-spezifikation.md)
und ihrer [Fallmatrix](20260909-michaela-spec-matrix.md). Es wurden keine
Supervisor-Dateien oder externen Systeme verändert.

Der gelesene gemeinsame
[Vertragsstand](</Users/activi/Documents/ChatGPT/EnergyWarm Supervisor/CONTRACTS.md>)
bestätigt weiterhin keine neue Revision. Die
[R-D-Entscheidungen](</Users/activi/Documents/ChatGPT/EnergyWarm Supervisor/DECISIONS.md>)
bleiben in ihrem dokumentierten Status. Die folgenden logischen Felder und
Wertemengen sind Vorschläge für ein gemeinsames Schema; weder Endpunktnamen noch
CRM-Enums werden als bereits vorhanden ausgegeben.

## Vorhandener Agentvertrag: belegter Umfang

| Operation | Heute vom Agenten gesendet | Heute lokal geprüfte Antwort / Grenze |
|---|---|---|
| Kundensuche `energy-get-kunde` | POST mit `kunden_id`, `room` | Antwort als Text; vollständige fachliche Bindungs-/Negativantwort noch nicht durch die heutige lokale Prüfung belegt. |
| Slots `get-termine` | POST mit `kunden_id`, `room`, `termin_art`, optional `von`, `tage` | Strukturierte Slots extrahieren; Art und zeitbezogene ID prüfen; Angebote bei Wechsel/Fehler entwerten. Keine belegte Angebotsrevision/Ablauf- oder Kapazitätsgarantie. |
| Buchung `book-termin` | POST mit `kunden_id`, `room`, `termin_art`, `slot_id`; `X-Idempotency-Key` aus Job/Room/Slot | Lokal `ok is True`, `buchung_status == "ok"`, nichtleere `calendar_event_id` verlangen. Beleg wird nicht vollständig als dauerhafte Operation im CallState gespeichert; kein Statusabfrage-/Umbuchungspfad. |
| Ergebnis `energy-call-result` | POST mit `kunden_id`, `room`, `outcome`, `results`, `diagnostics`; Idempotenzheader | `save_result` gibt den HTTP-Body ungeprüft zurück; HTTP 200 ist keine fachliche Speicherquittung. Outcome-Matrix deckt mehrere Endgründe nicht ab. |

Authentisierung verwendet bestehende Credential-/Environment-Referenzen. Keine
Secretwerte in diesem Paket. Statische Übereinstimmung der vier POSTs aus dem
Audit beweist keine aktuelle Erreichbarkeit, Authentisierung, Speicherung,
Kalenderwirkung oder spätere Anrufauslösung. Endpunkte für Datenupdate,
Wiederanruf ohne Slot, Operationstatus, Umbuchung und Human-Übergabe sind im
heutigen EnergyBackend-Protokoll nicht vorhanden.

## Gemeinsame Regeln für jeden Vorschlag

Die fachliche Operation und ihr Übermittlungsversuch werden getrennt. Eine
stabile Operationsreferenz bezeichnet denselben Kundenauftrag über Retries und
Jobneustarts hinweg; Job-ID und Attempt-ID bezeichnen konkrete Ausführungen.
Ihre Erzeugung und Vertrauensgrenze werden unter R-D-02/R-D-05 vom Supervisor
und den beteiligten Ownern festgelegt. Modellargumente liefern keine autoritative
Lead-, Call- oder Operationsidentität.

| Logisches Feld | Vorschlag für Typ / Pflicht / Nullregel |
|---|---|
| Vertragsrevision | Nichtleerer String, Pflicht bei jedem neuen Vertragsrequest und jeder Quittung. Empfängerunterstützung vor Versand belegt. Dies vergibt noch keine Revisionsnummer. |
| Stabile Call-/Operationsreferenz | Opaque nichtleere Strings, Pflicht bei Mutation und Statusklärung; vom zuständigen System erzeugt und auf Bindung geprüft. |
| Job-/Versuchsreferenz | Nichtleerer String für einen tatsächlich gestarteten Versuch; bei vorgemerkter, noch nicht gestarteter Wirkung darf der Ausführungsversuch fehlen. |
| Lead-/Personen-/Room-Bindung | Verifizierte Referenzen, für personenbezogene Mutation Pflicht. Bei technischem Abschluss ohne Lead nur sichere Call-/Job-Korrelation und expliziter Bindungsfehler. |
| Revision des Fachzustands | Monoton vergleichbare Revision bzw. konkurrierend prüfbarer Versionsbeleg; keine Uhrzeit allein als Überschreibregel. |
| Ergebnis einer Operation | Geschlossene Unterscheidung: angenommen/erledigt, sicher nicht ausgeführt, noch in Bearbeitung oder unklar. Konkrete Wirewerte durch Supervisor. |
| Wirkungsbeleg | Passende Operationsreferenz plus betroffene Ressource und bestätigte Revision/Zeit. Für „erledigt“ Pflicht, andernfalls kein erfundener Beleg. |
| Ursache / Lieferstand | Maschinenlesbarer vereinbarter Fehlergrund; technische Diagnose getrennt von kurzer kundenfähiger Erklärung. Keine rohen Antworten/Secrets im Dialog. |

Fehlende Angaben, explizit leere Werte und Löschungen müssen unterscheidbar sein:
Auslassen im Patch heißt „unverändert“, nicht „löschen“. `null` ist nur mit
passendem fachlichen Zustand zulässig, etwa ein unklarer nicht bekannter Wert.
Eine aktive Datenlöschung ist kein Nebenprodukt dieser Spezifikation. Arrays sind
leer, wenn belegbar keine Elemente vorliegen; „nicht abgefragt/unklar“ erhält einen
eigenen Zustand, statt als leeres Suchergebnis aufzutreten.

Die Pflichtfelder dürfen eine ungebuchte oder technisch fehlgeschlagene Sitzung
nicht zum Erfinden von Umsatz-, Zustimmungs- oder Buchungswerten zwingen.
Empfängerfehler, unbekannte Enumwerte und nicht unterstützte Revisionen werden
sicher abgewiesen bzw. zur vertraglich definierten Klärung erhalten; kein
stillschweigendes Mapping auf `interessiert`.

## SV01 — Ergebnis, Leadmarkierung und Kontaktstopp

**R-D-03/05/07; R02–R04/R12/R18/R19.** Producer: Agent/Call-Lifecycle;
Consumer: n8n/Persistenz, bei Sperre auch die Systeme für menschliche
StepEnergy-Vertriebsanrufe. Supervisor koordiniert; fachliche Bedeutung der
Sperre ist bereits entschieden, technische Verteilung nicht.

| Alt | Vorgeschlagene Erweiterung | Pflicht / Verhalten |
|---|---|---|
| Ein `outcome`, Interesse an AI-Buchung gekoppelt | Getrennte Dimensionen Gesprächsende, Interesse, Terminwunsch, Buchung, Kontaktstopp, Wiederanrufauftrag und Lieferstatus | Tatsächlicher Endgrund immer Pflicht; übrige Dimensionen explizit unbekannt/keiner statt erzwungen positiv. |
| `results` ohne vollständige Endpfadgarantie | Bestätigter Teilstand, Datenlücken, Zeitpräferenzen, Zustimmungsreferenzen und offene Operationen | Jeder terminale Matrixpfad lieferbar; fehlende Daten zulässig. |
| Keine dedizierte belegte Sperrquittung | Kontaktstoppumfang StepEnergy-Vertriebsanrufe AI + Mensch, auslösendes Ereignis, systemischer Annahme-/Wirksamkeitsbeleg | Sofort lokal blockieren; wiederholte Sperrübermittlung idempotent; bestehende Buchung separat erhalten. |
| Freitext-/Verkaufsstatus als Gesamtergebnis | Fachliche Anrufergebnis-/Leadaktionsabbildung pro M-Zeile | Wirewert-Mapping in einer versionierten Tabelle durch n8n-Owner/Supervisor; keine heutigen CRM-Werte behaupten. |

„Zielperson nicht erreicht“ bleibt Anrufergebnis. n8n entscheidet anhand seiner
bestehenden Regeln, ob eine erneute Einreihung erfolgt. Das gilt ebenso für die
nicht neu entschiedenen Retry-Zuordnungen bei Stille, Mailbox und Gesprächsabbruch.
Keine direkte Gleichsetzung mit „Wiederanrufen“. Kontaktstopp muss auch schon
geplante weitere StepEnergy-Vertriebsanrufe erreichen. Der Vertrag beschreibt,
wie deren Ausführung unterbunden wird, ohne Kalenderstorno als bereits erfolgt
auszugeben. Andere Werbekanäle werden nicht neu einbezogen.

**Fehlerfälle:** Empfänger nimmt Ergebnis an, Sperre aber noch nicht wirksam;
Ergebnis gespeichert, Antwort verloren; Bindung fehlt; unbekannter Endgrund;
Endevent doppelt; gebucht und anschließend abgebrochen/gestoppt. Keine einzelne
Quittung darf mehrere unbelegte Teilwirkungen als erledigt markieren.

**Migration:** Alte Ergebnisschemas lesbar halten. Bestehendes `interessiert`
nicht rückwirkend in ungeprüfte allgemeine Interessensbekundung umdeuten; die
jeweilige Quellrevision bestimmt die Semantik. Neue Kombinationen nicht verlusthaft
in alte Outcomes pressen. Rollout blockieren, bis der Empfänger die neue Matrix
akzeptiert; kein erfundener „Legacy-Erfolg“ als Fallback.

**Abnahme:** AC03/07–AC10/25/29/40–AC42/46; ein synthetisches vollständiges und ein
synthetisches ungebundenes technisches Ergebnis sowie gebucht+Kontaktstopp und
Wiederholung auf beiden Seiten prüfen.

## SV02 — Identität, bestätigte Kontakt-/Tarifrevision und Fortsetzungskontext

**R-D-02/07; R04/R05/R14/R16/R20.** Producer/Consumer: Agent und n8n-Kunden-/Lead-
und Dispatchwege. Eigenständige Beratung einer anderen Person benötigt eine
neue sichere Personenbindung; das ist keine einfache Kontaktkorrektur.

| Logischer Inhalt | Typ-/Pflichtvorschlag |
|---|---|
| Identitätsstatus | Geschlossene Kategorie gemäß Zustandsmodell; Herkunft Zielperson/Dritter/System getrennt. |
| Kontaktstand | Name, Ort und Rückrufnummer als optionale fachliche Felder mit letzter ausdrücklich bestätigter Revision. Pflichtnummer vor Buchung; fehlende Nummer ist keine erfundene Fallbacknummer. |
| Tarifstand | Objekt je gewünschter Sparte; Anbieter und Zählernummer als Strings; Verbrauch, Grund- und Arbeitspreis mit Zahlendarstellung, Einheit und Bezugszeit. Kein binärer „alles vollständig“-Ersatz. |
| Qualität je Feld | Verständlich/unklar/nicht verfügbar/verweigert sowie als ungefähr gekennzeichnete Angabe; unbekannter Wert darf `null` sein. |
| Herkunft/Revision | Bestätigte Kundenangabe, systemischer Altbestand oder Dritthinweis unterscheiden; letzte bestätigte Revision kontrolliert übernehmen. |
| Folgezweck | Datenergänzung, Fortsetzung bei Zeitmangel oder Terminabstimmung; nur bei tatsächlichem Folgewunsch/Auftrag vorhanden. |
| Fortsetzung | Ursprünglicher Human-Wunsch, offene Felder, bestätigte Daten, gewünschte Zeitfenster, Anrede und vorhandene Buchungs-/Operationsreferenzen |

Vorhandene Werte aus dem Backend sind nicht automatisch im jetzigen Gespräch
bestätigte Korrekturen. Die Kundenbestätigung wird nur festgehalten, wenn sie
tatsächlich vorliegt. Keine neuen Dokumenten-/Nachweispflichten für Kunden. Ein
geschätzter Verbrauch wird nicht als exakt ausgegeben. Der Betriebsmix 70/30
belegt keine konkrete Sparte eines einzelnen Kunden.

Bei neuem Call aktuelle Person/Bereitschaft klären und Kontext nur nach sicherer
Bindung übernehmen. Alte Gesprächserlaubnis, Dritthinweis und gebuchter AI-Termin
sind unterschiedliche Tatsachen. Ein beendeter Job wartet nicht bis zum Rückruf.
Fehlender oder veralteter Kontext wird nicht aus erfundenen Daten rekonstruiert.

**Fehlerfälle:** verspätete Antwort zu alter Kontaktrevision, gleiche Revision mit
anderem Inhalt, neue Person ohne bestätigte neue Bindung, verlorener Folgezweck,
einseitige Aktualisierung von Kunde und Kalenderempfänger. Letzte bestätigte
Fachrevision erhalten; tatsächliche Empfängerrevision separat ausweisen.

**Migration/Retention:** Bestehende unstrukturierte Tarifstrings nur eindeutig
zugeordnet migrieren; ansonsten Herkunft/Unklarheit behalten. Keine automatische
Strom-/Gasverteilung. Der lokale V3-Testvertrag `results.kontakt` ist kein
produktiver Vertrag. Retention, berechtigte Empfänger, Zugriffsschutz und
Persistenzort werden unter R-D-07 festgelegt; keine neue Speicherfrist erfinden.
Fachübergabe enthält notwendige Daten, Diagnostik bleibt redigiert.

**Abnahme:** AC10–AC13/17/30/31/35/36/43–AC46, insbesondere zwei Korrekturen mit
verzögerter Antwort auf die ältere Revision und Folgeanruf mit Terminabstimmungszweck.

## SV03 — Human-/AI-Angebot, Zustimmung und belastbarer Buchungsbeleg

**R-D-02/04/08; R08–R11/R13.** Producer: Agent; Consumer: n8n/Kalender.
Getrennte Human-/AI-Kalenderressourcen sind beschlossen. Konkrete Ressourcen,
Kapazität und Angebotsgültigkeit sind weiterhin zu belegen.

| Alt | Vorgeschlagene Präzisierung | Pflicht / Nullregel |
|---|---|---|
| Slot-ID `art|ISO-Zeit` plus Art | Slotreferenz, Angebotsrevision, zugeordnete Ressource/Art, zeitzonenbewusster Start/Ende, serverseitige Gültigkeit | Nur serverseitig gelieferte passende Angebote buchbar; keine erfundene Ablaufdauer. |
| Bestätigung aus letztem Text mit Teilstrings | Referenz auf konkretes Angebot und dessen bestätigte Art, Person/Nummer und Zeit; aktuell gültige Fach-/Kontaktrevision | Bestätigung muss zum tatsächlich geäußerten Angebot passen. Ein fremdes Ja autorisiert nichts. |
| Request mit Kunde/Room/Art/Slot | Stabile Buchungsoperation mit fachlichem Zweck und gültiger Bindung; konkrete Kundenbestätigung als Referenz | Neuer fachlicher Versuch braucht neue bestätigte Wahl; Retry gleicher Operation behält Identität/Inhalt. |
| `ok`, `buchung_status`, Event-ID | Korrelierte Operationsquittung mit Event-ID, Ressource/Art, kanonischem Start/Ende und tatsächlicher Bindung/Revision | Erfolg nur bei vollständiger passender Quittung; fehlendes Feld bedeutet nicht automatisch Nichtbuchung. |

Bei abweichendem serverseitigem Termin wird nicht still die ursprüngliche Wahl
als erfüllt bestätigt. Tatsächliche Wirkung intern erhalten und den Konflikt
klären; kein erneuter Commit ohne sichere Abgrenzung. Der aktuelle lokale
30-Minuten-Endzeitmechanismus ist Iststand, kein neuer gemeinsamer Dauerbeschluss.
R-D-08 muss bestätigen, ob diese Dauer für die jeweiligen Ressourcen gilt;
maßgeblich ist danach der angenommene kanonische Zeitraum. Sommer-/Winterzeit und
Zeitzone `Europe/Berlin` mit Offset werden anhand tatsächlicher Kalenderdaten
geprüft, keine lokalen Zeitstrings ohne Zuordnung buchen.

**Fehlerklassen:** erfolgreich leer; fehlerhafte Suche; Angebot abgelaufen;
sicher abgewiesener Slotkonflikt ohne Commit; unklarer Commit; falsche Event-/Call-
Zuordnung; gleichzeitige Buchungsversuche. „HTTP 409/500“ allein ist kein
vertraglicher Nicht-Commit-Beleg. Der Commitstatus muss eindeutig zugesichert
sein oder bleibt unklar.

**Migration:** Vorhandene Buchungen samt Belegen erhalten. Neue Belegfelder erst
nach Empfängerunterstützung verwenden. Keine neuen bestätigten Buchungen aus
alten Wünschen, Textbestätigungen oder reinen Terminstartern erzeugen. Alte
Slotformate nur gemäß angenommener Versionsregel lesen; keine Rückkonvertierung
auf ungesicherte Freitextzeiten.

**Abnahme:** AC16–AC24/27–AC29/32/43; fremde Event-ID, konkurrierender Slot,
Kalenderartwechsel, Angebotsablauf und abweichender kanonischer Zeitraum.

## SV04 — Wiederanruf ohne festen Slot und n8n-Folgeauftrag

**R-D-03/05/07; R12/R20.** Gilt für B25/M27. Producer: Agent;
Consumer und Ausführung: n8n. Kein zusätzlicher lokaler Scheduler.

| Vorgeschlagener Inhalt | Typ-/Pflichtvorschlag |
|---|---|
| Auftragsart | Explizit „Wiederanruf ohne Slot wegen Kalenderproblem“, getrennt von Kalenderbuchung. |
| Zustimmung | Positive tatsächliche Rückrufzustimmung mit Ereignis-/Kontextreferenz; Pflicht vor Übermittlung als Kundenauftrag. |
| Zweck | Terminabstimmung durch Michaela; Pflicht. |
| Fachliche Leadaktion | „Wiederanrufen“, konkrete API-Abbildung durch n8n; Pflicht für diesen angenommenen Auftrag. |
| Notiz | Kalenderproblem, Zustimmung, Termin noch offen; vorhandener Human-Wunsch und Datenstand referenziert. |
| Zeitpräferenzen | Optional; unverbindliche Präferenz getrennt von verbindlichem Termin. Kein `slot_id` oder behaupteter Terminzeitpunkt. |
| Kontext | Sichere Bindung plus bestätigte Daten-/Kontaktrevision und offene Fragen; Pflichtreferenz gemäß SV02. |
| Annahmebeleg | Auftrags-ID, Operations-ID und bestätigte Revision/Zustand; Pflicht vor „vorgemerkt“. |

Der Server muss Auftrag, Notiz und Kontext so annehmen, dass keine scheinbar
erfolgreiche Teilannahme einen nicht ausführbaren Rückruf hinterlässt. Ob dies
transaktional oder durch einen belegten zusammenhängenden Operationszustand
geschieht, ist technische Supervisorentscheidung. Ein Statuswrite ohne erhaltenen
Auftrag/Kontext beweist den vereinbarten Rückruf nicht.

Ohne Zustimmung kein Auftrag. Bei Kontaktstopp wird kein neuer Vertriebsanruf
gestartet. Bei verlorener Annahmeantwort denselben Auftrag intern klären. Ist
die Übergabe nicht verlässlich möglich, keine erfolgte Vormerkung oder konkrete
Zeit zusagen. Der technische Lieferfehler wird nach SV05 erhalten. Es gibt keine
Fallbackregel „stattdessen beliebigen AI-Slot buchen“.

**Abgrenzung:** Leere erfolgreiche Suche ohne passenden Termin bleibt B12/M26/M28;
unklarer Buchungscommit bleibt B22/M30. Der Sonderauftrag wird nicht auf diese
Fälle ausgedehnt. „Zielperson nicht erreicht“ erzeugt ihn ebenfalls nicht.

**Abnahme:** AC25/26/28/41/44/45. Gleichen Auftrag zweimal übermitteln, Antwort
verlieren, Folgejob mit korrektem Kontext starten und Nichtzustimmung/Stoppsignal
als Nullaktion prüfen. Termineintrag bzw. Annahmebeleg allein beweist keinen
tatsächlichen Folgeanruf.

## SV05 — Operationsjournal, Idempotenz, Statusklärung und Ergebnislieferung

**R-D-02/05/06/07; R13/R18/R19.** Producer: Agent und Lifecycle;
Consumer: n8n/Call-Controller/Persistenz. Der Supervisor bestimmt die konkrete
dauerhafte Zuständigkeit. Empfehlung: am vorhandenen Call-Controller-/n8n-
Verantwortungsbereich anschließen, keine zweite Leadwarteschlange in Michaela.

Eine Mutationsabsicht muss vor möglicher externer Wirkung dauerhaft und sicher
korrelierbar sein. Der Kunde bestätigt fachlich; anschließend werden konkrete
Operation, Payloadrevision und Bindung fixiert. Erst nach belegter dauerhafter
Registrierung darf die Mutation versendet werden. Diese Registrierung erzeugt
keine fachliche Buchung. Ist sie nicht verfügbar, sicher vor neuem Versand
stoppen. Ein optionales Eventlog oder `asyncio.shield` erfüllt diese Garantie nicht.

| Phase | Zulässiger nächster Schritt | Nicht zulässig |
|---|---|---|
| Fachlich bestätigt, noch nicht abgesendet | Absicht dauerhaft registrieren; bei widerrufener/überholter Zustimmung verwerfen, ohne Commit. | Buchungserfolg behaupten. |
| Absicht gespeichert, Versand ausstehend | Unter gültigen Schranken dieselbe Operation ausführen bzw. vor Versand stoppen. | Aus unbekanntem Versandstatus eine neue Operation starten. |
| Versand erfolgt, Antwort fehlt | Status derselben Operation lesen/reconciliieren; unklar erhalten. | Erfolg, sichere Nichtausführung, neuer Slot oder neuer Schlüssel auf Verdacht. |
| Passender Wirkungsbeleg | Tatsächlichen Zustand/Beleg dauerhaft sichern und nur diese Wirkung bestätigen. | Fremde/falsche/alte Quittung auf neue Revision anwenden. |
| Sicher nicht ausgeführt | Fachlichen Fehler erhalten; neue Aktion nur aus weiterhin gültigem bzw. neu bestätigtem Kundenauftrag. | Widersprüchliche Wirkung ignorieren oder unklare Antwort als sicher negativ behandeln. |
| Dauerhaft offen | Zuständiger Recoveryprozess klärt ohne erforderliche lebende Gesprächssitzung. | Neuer Klärungsanruf oder Buchung aus Recovery erfinden. |

**Deduplizierungsvorschlag:** Schlüssel umfasst stabile fachliche Operation und
bezeichnete Revision, nicht nur den vergänglichen Job. Gleicher Schlüssel mit
gleichem Inhalt liefert denselben Operationsstand; gleicher Schlüssel mit
abweichendem Inhalt wird abgewiesen. Wiederholungsversuche sind referenziert und
ändern nicht den Auftrag. Neue Kundenkorrektur ist eine neue korrelierte
Operation/Revision; sie darf nicht unter dem Schlüssel des alten Inhalts
versendet werden. Die tatsächlich eingesetzte Datenbank muss atomare
Unique-/Transaktionsgarantien belegen; Header allein reicht nicht.

**Statusklärung:** Read-only-Abfrage nach Operation bzw. tatsächlicher externer
Referenz, soweit der Vertrag dies zulässt. „Nicht gefunden“ ist nur dann sicher
„nicht ausgeführt“, wenn die Systemgarantien das nach laufenden/verzögerten
Ausführungen belastbar ausschließen. Sonst bleibt der Vorgang offen. Konkrete
Abfrageintervalle, Betriebsfristen und Alarmempfänger werden nicht erfunden.
Unauflösbare Operationen brauchen einen benannten internen Owner und sichtbaren
Bearbeitungsstand; keine technische Kundenklärung gemäß B22.

**Ergebnislieferung:** Ein terminaler fachlicher Snapshot pro Call wird
idempotent angeboten und nach Speicherquittung als angenommen markiert. Die
Quittung nennt Ergebnisreferenz und bestätigte Revision; HTTP-Erfolg allein
genügt nicht. Der Snapshot hält unklare Operationen ehrlich fest. Spätere
Auflösungen sind korrelierte Ergänzungen desselben Vorgangs, keine zweite
Vertriebsentscheidung. Ist bereits ein terminaler Snapshot gespeichert, darf
eine verspätete ältere Version ihn nicht überschreiben. Unbestätigte oder sicher
abgelehnte Speicherung bleibt lieferbar/reparierbar nach Vertrag.

**Fehlender Gesamtspeicherweg:** Vorhandene dauerhafte Absichten bleiben beim
zuständigen Dienst auffindbar. Sind alle angenommenen dauerhaften Wege vor
Registrierung unerreichbar, keine neue Mutation; kontrollierter technischer
Abschluss, keine falsche Vormerkung. Ohne implementierten dauerhaften Weg kann
Prozessverlust mit Erhalt sämtlicher Teilangaben nicht als bestanden gelten.
Diese Lücke muss vor Produktionsabnahme geschlossen werden, nicht durch
provisorische PII-Dateien oder eine ungeprüfte lokale Queue verdeckt werden.

**Migration/Rückweg:** Neue und alte Jobs/Ergebnisse korrelierbar halten; alte
Idempotenzschlüssel nicht blind neu ausstellen. Produktrollback nimmt externe
Wirkungen nicht zurück. Noch offene Operationen weiterhin mit ihrer ursprünglichen
Revision klären, auch wenn der sendende Agent inzwischen zurückgerollt wurde.

**Abnahme:** AC26–AC29/34/40–AC43/46, jeweils vor Versand, nach Commit vor Antwort,
nach Quittung vor Fachzustandsupdate, beim Export, nach Jobneustart sowie bei
zwei parallelen Versuchen. Frische Integrationsbelege der Persistenz erforderlich.

## SV06 — Bestätigte Datenänderung und sichere Umbuchung

**R-D-02/04/05/07/08; R14/R15.** Producer: Agent; Consumer: n8n/Kundendaten/
Kalender. Datenänderung und Terminänderung sind verschiedene Operationen.

Ein Datenupdate enthält betroffene Felder/Sparte, bestätigte neue Revision,
erwartete bisherige Empfängerrevision und passende Personenbindung. Auslassen
heißt unverändert. Eine positive Updatequittung muss genau die angenommenen
Felder/Revision nennen. Kundenaussage allein beweist keine Datenbankänderung;
erfolgreiche Speicherung beweist noch keine Weitergabe an alle benötigten
Empfänger. Der Vertrag legt diese Empfänger und ihre Belege fest.

Eine sichere Umbuchung benötigt bestehenden Buchungsbeleg samt aktueller Version,
neuen serverseitig angebotenen Slot, konkrete Zustimmung zu Person/Nummer/Art/Zeit,
Operationsreferenz und Schutz vor Konkurrenz. Die Quittung beschreibt den
tatsächlichen Zustand der alten und neuen Buchung. Vorher ist nur die bisherige
Buchung belegt; bei unklarem Wechsel bleiben letzter Beleg und mögliche neue
Wirkung ausdrücklich nebeneinander erhalten. Es wird nicht behauptet, der alte
Termin sei sicher noch aktiv, falls der Umbuchungscommit dies bereits verändert
haben könnte.

**Sicherheitsbedingung:** Kein Zwischenzustand „alter Termin gelöscht, neuer
Termin vielleicht fehlgeschlagen“ ohne nachgewiesenen sicheren vertraglichen
Weg. Wenn eine atomare Änderung oder ein gleichwertig abgesicherter Prozess
nicht verfügbar ist, SV07 statt selbst gebautem Löschen/Neuanlegen. Keine neue
Stornierungsbefugnis aus einem allgemeinen Korrekturwunsch ableiten.

**Fehlerfälle:** falsche Person, veraltete Kunden-/Eventrevision, Slot inzwischen
belegt, sichere Nichtausführung, Antwortverlust nach Wirkung, nur ein Empfänger
aktualisiert. Kunde hört nur belegten Teilfortschritt; übrige Wirkung bleibt
offen. Eine sicher gescheiterte Umbuchung lässt den bisherigen Termin erhalten;
ein unklarer Ausgang muss intern geklärt werden und darf nicht durch eine
Ersatzbuchung ergänzt werden.

**Migration:** Feature nur auf akzeptierter Empfängerrevision anbieten. Bestehende
Buchungsbelege übernehmen, nicht aus Terminfeldern neue Event-IDs erfinden.
Rollback erhält Datenrevisionen und externe Änderungen; keine Rücksetzung auf
ältere Kundenangaben durch Agentcode-Rollback.

**Abnahme:** AC30–AC34/43. Ein positiver Datenupdate, teilweise Weitergabe,
konkurrierendes Update, bestätigte Umbuchung, fehlende sichere Fähigkeit und
Commit-Timeout sind getrennte Fälle.

## SV07 — Menschliche Übergabe eines Änderungswunsches

**R-D-03/05/07; R14/R15.** Producer: Agent; Consumer: der noch konkret zu
benennende menschliche Bearbeitungsweg unter n8n-/Supervisorverantwortung.
Der bestätigte Fachwunsch erlaubt menschliche Bearbeitung bei fehlender sicherer
Umbuchung. Eine neue Supportadresse, Mail, Person oder Live-Transfer-Funktion
wird hier nicht erfunden.

Pflichtinhalt: sichere Lead-/Personenreferenz, bestehender Terminbeleg soweit
vorhanden, bestätigter Änderungswunsch, aktuelle Kontakt-/Datenrevision,
Operationsreferenz und tatsächlicher Buchungs-/Änderungsstatus. Annahmebeleg:
Übergabereferenz, zuständiger Bearbeitungsweg und angenommene Revision. Das
bestätigt die Übergabe, noch nicht die gewünschte Umbuchung oder einen Zeitpunkt
der menschlichen Bearbeitung.

Fehlender Empfänger, negative Annahme oder Antwortverlust führen nicht zu „ich
habe es weitergegeben“. Wunsch und Lieferstatus erhalten, bestehende Buchung
nicht löschen. Keine Bearbeitungsfrist und kein zusätzlicher Rückruf versprechen,
die nicht durch den angenommenen Vertrag gedeckt sind. Unklarer
Umbuchungsausgang wird zuerst als solche Operation geklärt; menschliche
Bearbeitung darf keine zweite unabhängige Ersatzbuchung starten.

Migration: Fähigkeit nur nach festgelegtem Empfänger und Annahmevertrag
freischalten. Abnahme: AC31/33/34/41/43 mit erfolgreicher Annahme, sicherer
Ablehnung, Antwortverlust und wiederholter gleicher Übergabe.

## SV08 — Call-Lifecycle, Telefonieereignisse und Folgejob

**R-D-01/02/05/06; R17/R18/R20/R22.** Producer/Consumer: LiveKit, n8n,
verpflichtender Call-Controller und PBX im jeweils freigegebenen Scope.

Erforderlich sind stabile Call-ID, Job-/Room-/Teilnehmerzuordnung, signierte bzw.
anderweitig vertraglich authentisierte Events mit Event-ID, tatsächlicher
Endgrund, Reihenfolge/Revision und idempotente Ergebnisannahme. AgentShutdown,
Medienende, Raumende, Fachabschluss und gespeichertes Ergebnis sind eigene
Ereignisse. Ein fehlender Sessionreport darf das Fachresultat nicht verhindern;
ein Startupfehler ohne Session benötigt einen technischen Abschluss beim
zuständigen Controller/Startpfad.

Mailbox ohne Nachricht; Nichtannahme nach sieben bis acht tatsächlich belegten
Ringzyklen; Besetzt/Abweisung nach bestehender n8n-Politik. Ein PBX-Timer darf
Ringzyklen nur bei belegter Kadenz ersetzen. Ereignisse nach bereits angenommener
Verbindung oder nach terminalem Versuch dürfen keine doppelte erneute
Einreihung auslösen. V3 LocalCallConnection/SQLite sind Testprototypen, keine
nachgewiesene produktive Telefonieanbindung.

Beim Folgejob n8n-Auftrag, Zweck, Kontextrevision, aktuelle Bindung und vorhandene
Buchungs-/Operationsreferenzen erhalten. Kontaktstopp vor neuem Vertriebsanruf
beachten. Aus einem Kalendertermin alleine lässt sich kein erfolgter SIP-Anruf
ableiten. Providerersatz muss Zustand erhalten; ohne funktionierenden Ersatz
Verbindung beenden, ohne notwendige TTS-Abschiedsrede.

**Migration/Abnahme:** Aktive Zielversionen und Eventrevisionen je Stack benennen;
alte/verzögerte Events sicher zuordnen. AC29/38–AC42/44–AC47. Später getrennt
autorisierte reale Fälle für Medienende vor/nach Ergebnis, doppeltes Event,
Startupfehler, Providerersatz, Ende ohne TTS und Folgeanruf mit korrektem Zweck.
Keine Provider-/Telefonieaktion ist durch diesen Entwurf autorisiert.

## Welche positive Systembestätigung ist für welche Aussage nötig?

| Aussage/Aktion | Erforderlicher positiver Beleg | Was nicht reicht |
|---|---|---|
| „Der Human-/AI-Termin ist gebucht“ | Passende Buchungsoperation mit Event-ID, Art/Ressource, kanonischem Zeitraum und Bindung. | Zustimmung, angebotenes Zeitfenster, Toolaufruf, HTTP 200 oder bloß nichtleere Antwort. |
| „Der Rückruf ist vorgemerkt“ ohne Slot | Angenommener Rückrufauftrag mit Zustimmung, Zweck, Notiz und gesichertem Fortsetzungskontext. | Leadnotiz alleine, lokales Flag oder ein Kundenwunsch. |
| „Die Daten sind geändert“ | Updatequittung für betroffene bestätigte Datenrevision. | „Ja, die neue Nummer stimmt“ oder nur Aufnahme im Chat. |
| „Ich habe die Änderung weitergegeben“ | Annahmebeleg des vereinbarten Empfängerwegs für diese Revision. | Erfolgreiche Kundenpersistenz ohne Weitergabebeleg. |
| „Der Termin ist umgebucht“ | Korrelierte Umbuchungsquittung mit tatsächlichem Alt-/Neuzustand. | Neue Zeitpräferenz oder zweites Slotangebot. |
| „Der Kontaktstopp ist hinterlegt/wirksam“ | Passende Sperrannahme bzw. Wirksamkeitsbeleg für StepEnergy-Vertriebsanrufe AI + Mensch. | Dialog lokal beendet oder Export nur gestartet. |
| „Ergebnis gespeichert“ im technischen Bericht | Fachliche Ergebnisquittung und passende gespeicherte Revision. | Nicht geworfene HTTP-Ausnahme. |
| „Folgeanruf erfolgt“ | Tatsächlicher Call-/Dispatch-/Telefonienachweis gemäß SV08. | Kalenderbuchung oder angenommener Wiederanrufauftrag. |
| „Vergleich berechnet“ | Beleg des zuständigen vereinbarten Berechnungswegs für die tatsächlichen Eingaben. | Drei vorhandene Kerndaten oder ein Human-Termin. |

## Übergabe an den Supervisor und Gates

SV01–SV08 benötigen je betroffener Schnittstelle denselben akzeptierten Stand
auf Producer- und Consumerseite: genaue Wirefelder/Enums, Pflicht-/Nullregeln,
Credentialreferenzen, Fehlerantworten, synthetische positive/negative Beispiele,
Revisionserkennung und Migrations-/Rollbackregeln. Erst der Supervisor
veröffentlicht nach Prüfung eine gemeinsame Revision unter seiner bestehenden
Vertragsablage. Die hier vorgeschlagenen Namen sind keine Abkürzung dieser Prüfung.

Unabhängige lokale Spezifikation und genehmigte V3-Fake-Tests können vorbereitet
werden. Reale Agentintegration und Erfolgsmeldungen der betroffenen Fähigkeit
bleiben bis zum Empfängernachweis blockiert. Fachentscheidungen F01–F10 sind dafür
nicht erneut zu stellen; zu klären sind technische Verträge und ihre Umsetzung.
