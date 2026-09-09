# ADR 0003: Menschlicher Termin nach Kundenwunsch oder vorhandenen Kerndaten

Status: Accepted (2026-09-09), präzisiert in Runde 8, ergänzt um Kalenderfallback in Runde 9 und teilweise fehlende Gasdaten in Runde 11 sowie reine Gasberatung in Runde 12. Keine Produktimplementierung.

## Kontext und Entscheidung

Entscheider: Nutzer/Projektauftraggeber in Sollablauf-Aufgabe `01a08728-6fe6-7793-abd8-bc0649c64ff7`, Runden 7–8. Maßgeblich ist die jüngste ausdrückliche Präzisierung in Runde 8:

- Ein menschlicher Termin ist fachlich freigegeben, wenn der Kunde ihn ausdrücklich wünscht, auch bei fehlenden Tarifdaten. Dieser Wunsch hat Vorrang vor der Datenergänzung durch einen AI-Rückruf.
- Ohne einen solchen ausdrücklichen Wunsch kann Michaela den menschlichen Termin anbieten, sobald aktueller kWh-Preis, Grundpreis und Jahresverbrauch vorliegen. Der Termin dient der Vergleichsbesprechung und dem möglichen Vertragsabschluss.
- Anbieter und Zählernummer sind keine Voraussetzung für den menschlichen Termin. Sie werden weiterhin erfragt, können aber beim menschlichen Termin ergänzt werden.
- Ergänzung Runde 11: Möchte der Kunde Strom und Gas vergleichen und liegen die drei Strom-Kerndaten vor, darf Michaela den menschlichen Termin auch bei noch unvollständigen Gasdaten anbieten. Sie bittet den Kunden, die fehlenden Gasangaben bis zum Termin vorzubereiten. Vorhandene Gaswerte und offene Angaben werden ausdrücklich übergeben; es wird kein bereits fertiger Gasvergleich behauptet. Nutzerbeleg: „Ja sie darf das und soll den kundne bitten die gas parameter bis zum nächsten termin vorzubereiten“.
- Ergänzung Runde 12: Wünscht der Kunde ausschließlich einen Gasvergleich, erfasst Michaela nur Gasdaten. Dieselbe Human-Freigabe gilt: ausdrücklicher Human-Wunsch ODER aktueller Gas-kWh-Preis, Gas-Grundpreis und Gas-Jahresverbrauch. Stromangaben sind dafür nicht erforderlich. Nutzer bestätigt die entsprechende Frage mit „ja natürlich“.
- Ergänzung Auswahl Nr. 4, Option A: Beim gewünschten Strom- UND Gasvergleich erlauben auch vollständige Gas-Kerndaten bei fehlenden Stromangaben ein Human-Angebot. Michaela bittet, die fehlenden Stromangaben bis zum Termin vorzubereiten. Damit gilt die Regel symmetrisch: Die drei Kerndaten mindestens einer gewünschten Energieart reichen für das Angebot; Werte und Lücken der anderen Sparte bleiben getrennt. Kein fertiger Vergleich der unvollständigen Sparte und keine zusätzliche Vorbereitungsgarantie als Buchungsschranke.
- Hat der Kunde Kerndaten nicht griffbereit oder gerade keine Zeit und wünscht nicht ausdrücklich den menschlichen Termin, vereinbart Michaela mit ihm einen AI-Rückruf zur Fortsetzung beziehungsweise Datenerfassung.

Die bestehenden Regeln zu ausdrücklicher Zustimmung, angebotenen echten Slots, konkreter Terminbestätigung und belegtem Buchungserfolg gelten für beide Terminarten weiter. Die drei vorhandenen Angaben erlauben ein Human-Angebot, keine Buchung ohne Zustimmung. Ein allgemeines Ja zum Tarifcheck ist kein ausdrücklicher Wunsch nach einem Menschen. Eine fehlende Gesprächserlaubnis allein erzeugt weiterhin keinen Rückrufwunsch.

## Ersetzte Alternative und Auswirkungen

Runde 4 erlaubte menschliche Termine allgemein trotz fehlender Tarifdaten (B07); Runde 6 bestätigte dies bei verweigerten Einzelangaben (B09). Runde 7 band den Human-Termin zunächst an vollständige erforderliche Daten (B10). Runde 8 präzisiert die gültige Alternative: ausdrücklicher Human-Wunsch ODER die drei Kerndaten. Diese Regel ersetzt die widersprechenden Pauschalformulierungen der früheren Runden. Datenverweigerung wird weiterhin ohne Druck respektiert und nicht als automatische Ablehnung der gesamten Beratung interpretiert.

Der ausdrückliche Wunsch nach einem Menschen wird nicht wegen fehlender Tarifwerte abgewiesen oder in einen AI-Rückruf umgedeutet. Der menschliche Ansprechpartner erhält vorhandene Werte und tatsächliche Datenlücken. Es wird weder ein vollständiger Vergleich noch ein erfolgreicher Vertragsabschluss erfunden. Für vorübergehend nicht verfügbare Kerndaten ohne Human-Wunsch bleibt der vereinbarte AI-Rückruf vorgesehen; keine automatische Wiederanrufserie bei dauerhaft verweigerten Angaben.

## Kein passender menschlicher Slot: bestätigte Ergänzung aus Runde 9

Der Nutzer beantwortet die Frage nach Übernahme der vorgeschlagenen Reihenfolge in den Sollablauf mit „ja bau das so“. Im geltenden Sitzungsumfang bestätigt dies die fachliche Regel und ihre Dokumentation, keine Produktimplementierung oder Kalenderaktion.

1. Zuerst mit dem Kunden einen anderen passenden Zeitraum klären und erneut im menschlichen Kalender suchen.
2. Ist weiterhin nichts Passendes verfügbar, einen echten freien AI-Slot zur späteren Terminabstimmung anbieten. Nur nach ausdrücklicher Zustimmung zum zusätzlichen AI-Gespräch und zum konkreten Termin buchen. Wer ausschließlich mit einem Menschen sprechen möchte, wird nicht automatisch auf AI umgestellt.
3. Rückrufzweck, ursprünglichen Human-Wunsch, vorhandene bestätigte Daten und gewünschte Zeitfenster erhalten. Beim Folgeanruf die Terminabstimmung fortsetzen, ohne bereits abgeschlossene Tarifaufnahme zu wiederholen. Der gebuchte AI-Rückruf garantiert keinen künftig freien Human-Slot.
4. Passt auch kein AI-Termin oder wird er abgelehnt, keinen Termin behaupten. Der ungebuchte Terminwunsch benötigt einen vollständigen Ergebnisweg; eine nicht vorhandene Nachbearbeitung wird nicht versprochen.

Die vorhandenen Human-/AI-Kalenderwege werden verwendet. Es wird keine eigene zusätzliche Wiederanrufverwaltung oder dauerhaft wartende Michaela-Sitzung eingeführt. n8n bleibt für den späteren Anrufstart zuständig; die tatsächliche Kette aus AI-Buchung, neuem Anruf und korrekter Gesprächsfortsetzung muss separat nachgewiesen werden.

Diese Reihenfolge gilt für eine erfolgreiche Kalendersuche ohne passenden Slot. Kalenderausfall und unklarer Buchungsausgang bleiben getrennte Fehlerfälle. Insbesondere kein zweiter Termin als blinder Ersatz nach möglichem Buchungscommit.

## Noch offene Konkretisierung der Berechnung und Sonderfälle

Die fachlichen Kerndaten für die Terminfreigabe sind beschlossen: aktueller kWh-Preis, Grundpreis und Jahresverbrauch. Das beweist keine technische Vollständigkeit sämtlicher Eingaben einer Vergleichsberechnung. Die geltenden Vergleichs-/Backendanforderungen müssen separat belegt werden; Anbieter und Zählernummer dürfen dabei nicht entgegen der Fachentscheidung zu zusätzlichen Terminpflichten werden.

Bei verweigerten Kerndaten verlangt der Nutzer in Nr. 5 Einwandbehandlung und eine verständliche Erklärung des Datenbedarfs. Der Folgeschritt ist durch die spätere Bestätigung zu Nr. 5 entschieden: Einmal menschliche Beratung anbieten, bei Zustimmung nach den bestehenden Buchungsregeln einen Human-Termin vereinbaren, andernfalls freundlich beenden. Die Zustimmung zu diesem konkreten Angebot erfüllt den Human-Wunsch trotz Datenlücken. Eine Datenverweigerung allein ist keine Gesamtablehnung. Fehlende Slots oder Kalenderfehler folgen den bereits bestätigten Alternativwegen; keinen Termin erfinden. Der Fall vollständiger Strom-Kerndaten mit unvollständigen Gasdaten ist durch Runde 11 entschieden; Reine Gasberatung ist durch Runde 12 erlaubt. Der umgekehrte Teilfall bei gewünschtem Strom- UND Gasvergleich ist durch Auswahl Nr. 4A ebenfalls entschieden: vollständige Gas-Kerndaten erlauben Human mit Bitte, die fehlenden Stromangaben vorzubereiten. Vollständige Eingabedaten sind kein Beleg einer bereits erfolgreich ausgeführten Berechnung. Zuständigkeit, Berechnungsbeleg und Verfügbarkeit des Vergleichs zum menschlichen Termin werden im gemeinsamen Vertrag geklärt. Bei ausdrücklichem Human-Wunsch sind fehlende Kerndaten bereits als zulässige Ausnahme entschieden.

## Korrekturen nach erfolgreicher Buchung: Auswahl Nr. 10A

Der Nutzer bestätigt ausdrücklich „Nr 10 auswahloption A“. Bestätigte Kontakt- und Tarifdatenkorrekturen werden übernommen und an die betroffenen Empfänger weitergegeben. Terminänderungen bearbeitet Michaela selbst, wenn eine sichere Umbuchung verfügbar ist; andernfalls übergibt sie den Änderungswunsch an einen Menschen. Ohne belegten Erfolg wird keine Änderung als durchgeführt bestätigt.

Bestätigte Kundenaussage, tatsächlich gespeicherte Daten und tatsächlicher Buchungszustand müssen unterscheidbar bleiben. Eine geänderte Zeitpräferenz ist noch kein umgebuchter Termin. Die bestehenden Regeln zu Personenbindung, angebotenen Slots und konkreter Zustimmung gelten auch für eine Umbuchung. Bei unklarem Ergebnis gilt B22/lokales ADR 0005, insbesondere keine blinde Doppelbuchung. Der sichere Umbuchungs- und Übergabeweg ist eine technische Voraussetzung, keine in dieser Sitzung nachgewiesene Funktion. Auch eine Übergabe darf erst nach belegter Annahme als erfolgt bestätigt werden.

Die spätere Abnahme umfasst Datenkorrektur nach Buchung, erfolgreiche bestätigte Umbuchung, Übergabe bei fehlender sicherer Umbuchungsfunktion und Fehler-/Abbruchpfade ohne erfundene Änderungsbestätigung. Gemeinsame Update-/Übergabeverträge bleiben Supervisor-Vorschläge.

## Umsetzung, Migration und Rückweg

Betroffen sind Datenerfassung, Outcome-/Terminartwahl und Buchungsprüfung. Der Zustand muss die Vollständigkeit der Kerndaten und den ausdrücklichen Human-Wunsch getrennt erhalten. Die fachliche Freigabe lautet Human-Wunsch ODER vollständige Kerndaten; Personen-/Call-Bindung und konkrete Terminbestätigung bleiben zusätzlich erforderlich.

Ein späterer AI-Rückruf muss die vorhandenen bestätigten Angaben für die Fortsetzung erhalten; der dafür erforderliche Gesprächs- und Persistenzvertrag bleibt zu spezifizieren. Gemeinsame EnergyWarm-Verträge werden dem Supervisor nur vorgeschlagen. Technische Vorbereitung und Übernahme folgen ADR-005. Bereits gebuchte Termine werden durch dieses Dokument weder geändert noch storniert; eine Migration oder Rücknahme muss solche Bestandsbuchungen ausdrücklich berücksichtigen.
