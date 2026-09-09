# ADR 0005: Kalenderausfall und unklarer Buchungsausgang

Status: Accepted (2026-09-09), fachliche Entscheidung; keine Produktimplementierung. Dieses lokale ADR ist nicht das gemeinsame EnergyWarm-ADR-005 zum V3-Vorbereitungsweg.

## Kontext und Entscheidung

Entscheider: Nutzer/Projektauftraggeber in Sollablauf-Sitzung `01a08728-6fe6-7793-abd8-bc0649c64ff7`, Auswahl Nr. 6 und eigene Vorgabe Nr. 7.

Die spätere ausdrückliche Korrektur zu Nr. 6 ersetzt die zunächst delegiert ausgewählte Option B: Michaela erklärt dem Kunden, dass es gerade Probleme mit dem Kalender gibt, und vereinbart einen späteren eigenen Rückruf zur Terminabstimmung. Der Lead wird auf „Wiederanrufen“ mit entsprechender Notiz gesetzt. Die bestehende Regel, AI-Rückrufe nur mit Kundenzustimmung zu vereinbaren, bleibt erhalten. Bei Ablehnung kein Wiederanrufauftrag.

Dies ist ein Rückrufauftrag ohne festen Kalendertermin. Es wird kein Slot erfunden oder ein gebuchter AI-Termin behauptet. Die Notiz hält Kalenderproblem, Zweck „Terminabstimmung durch Michaela“, Zustimmung und noch ausstehende Terminvereinbarung fest. Bestätigte Kontaktdaten, Tarifangaben, ursprünglicher Human-Wunsch und vorhandene Zeitpräferenzen bleiben für die Fortsetzung erhalten. Beim späteren Anruf setzt Michaela die Terminabstimmung fort. Es wird kein Zeitpunkt zugesagt, der nicht vereinbart und verlässlich unterstützt ist.

„Wiederanrufen“ bezeichnet den fachlichen Leadstatus; ein tatsächlicher technischer Statuswert oder ein bereits funktionierender Wiederanrufweg wird hier nicht behauptet. Der bestehende n8n-Verantwortungsbereich bleibt für Planung und Auslösung zuständig. Status, Notiz und Fortsetzungskontext müssen zuverlässig übergeben werden; die gemeinsame Vertragsänderung ist nur ein Vorschlag für den Supervisor. Fällt auch der Speicher-/Übergabeweg aus, darf Michaela keine erfolgreiche Vormerkung behaupten. Wiederherstellung und Ergebnisabgabe sind technische Spezifikationsarbeit.

Bei Nr. 7 verlangt der Nutzer: „diesen Punkt nicht mit dem Kunden besprechen“. Michaela führt mit dem Kunden keine technische Diskussion über unklare Buchungsausgänge und bietet dafür keinen neuen Klärungsrückruf an. Der Ausgang bleibt intern als unklar erhalten und ist technisch aufzulösen. Nur ein positiver Buchungsbeleg erlaubt eine Erfolgsbestätigung; ohne sicheren Nachweis darf weder Erfolg noch Nichtbuchung behauptet werden. Auch auf direkte Nachfrage wird kein unbewiesener Status behauptet. Keine blinde zweite Buchung oder Ersatzbuchung. Die spätere Nutzerantwort „7 ja mach das so“ bestätigt diese Regel erneut. Sie übernimmt nicht den Wiederanrufweg aus Nr. 6 für unklare Buchungen; die beiden Fälle bleiben getrennt.

## Alternativen und Folgen

Die frühere Option B „ohne Rückrufzusage abschließen“ ist für Kalenderausfall ausdrücklich verworfen. Gewählt ist ein späterer Rückruf durch Michaela mit Leadstatus und Notiz, kein zusätzlicher menschlicher Klärungsprozess. Das bereits bestätigte Vorgehen bei erfolgreicher Kalendersuche OHNE passenden Slot bleibt bestehen (lokales ADR 0003). Eine fehlgeschlagene Abfrage und eine bereits ausgelöste Buchung mit unklarem Ergebnis sind verschiedene Zustände.

Interne Statusklärung, Idempotenz und vollständige Ergebnisabgabe bleiben technische Anforderungen. Dieses ADR legt keinen nicht vorhandenen Backendprozess als funktionierend fest. Gemeinsame Verträge werden nur dem Supervisor vorgeschlagen.

## Abnahme und Übernahme

Kalenderausfall erzeugt bei Zustimmung einen verlässlich übergebenen Wiederanrufauftrag mit passender Notiz, aber keinen erfundenen Slot oder fälschlich bestätigten Kalendertermin. Ablehnung erzeugt keinen Wiederanrufauftrag. Der Folgeanruf setzt die Terminabstimmung mit erhaltenem Kontext fort. Unklarer Buchungsausgang erzeugt weder Doppelbuchung noch erfundenes positives oder negatives Buchungsergebnis; der tatsächliche Zustand übersteht das Gesprächsende. Kundenseitig findet keine technische Klärungsdiskussion statt. Die spätere Spezifikation muss diesen Abschluss mit dem tatsächlichen Buchungszustand konsistent ausgestalten.

Technische Änderungen und Übernahme folgen dem gemeinsamen EnergyWarm-ADR-005. Hier werden ausschließlich fachliche Entscheidungen dokumentiert.
