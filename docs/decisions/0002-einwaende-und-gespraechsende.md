# ADR 0002: Einwandbehandlung mit eindeutigem Gesprächsende

Status: Accepted (2026-09-09), fachliche Entscheidung; noch nicht implementiert.

## Kontext

Michaela soll als professioneller SDR Einwände bearbeiten. Der bestehende Code vermischt fehlende Gesprächserlaubnis mit Interesse und AI-Rückruf. Eine feste Drei-Nein-Regel ist nicht verbindlich dokumentiert und wird nicht eingeführt.

## Entscheidung und Beleg

Entscheider: Nutzer/Projektauftraggeber in der Sollablauf-Sitzung `01a08728-6fe6-7793-abd8-bc0649c64ff7`.

1. Auf das Beispiel „Ich bin mit meinem Anbieter zufrieden“ verlangt der Nutzer: „Einwand kurz aufgreifen und mit einwandbehandlung wie ein profesioneller SDR für Telesales“. Michaela darf den konkreten Vorbehalt aufgreifen und professionell bearbeiten; dies bedeutet keine unbegrenzte Überredung und kein erfundenes Preisversprechen.
2. Der Nutzer bestätigt anschließend mit „Diese Grenze übernehmen“: Ein erstes „Kein Interesse“ darf mit einer kurzen, passenden Klärung aufgegriffen werden. Bestätigt die Person danach ihre Ablehnung, beendet Michaela freundlich. „Nicht mehr anrufen“, „Lassen Sie mich in Ruhe“ und eine Aufforderung aufzulegen beenden den Vertriebsdialog sofort.
3. Der ursprüngliche Sitzungsauftrag verlangt ausdrücklich, fehlende Gesprächserlaubnis nicht automatisch als Interesse einzuordnen und nur ausdrücklich gewünschte AI-Rückrufe zu vereinbaren.

4. Auswahl Nr. 3, Option A: „Nicht mehr anrufen“ unterbindet weitere StepEnergy-Vertriebsanrufe durch AI und Menschen. Eine Sperre weiterer Werbekanäle wurde nicht gewählt. Das aktuelle Vertriebsdialogende gilt sofort.
5. Eigene Vorgabe zu Nr. 5: Bei verweigerten Kerndaten greift Michaela den Einwand auf und erklärt verständlich, wofür die betreffende Angabe im Vergleich benötigt wird. Die bereits bestätigten Einwandgrenzen gelten weiterhin. Anbieter und Zählernummer dürfen nicht entgegen ADR 0003 als Pflicht für die Human-Terminfreigabe dargestellt werden. Bleibt lediglich die Datenverweigerung bestehen, ist dies weiterhin keine automatische Gesamtablehnung. Der Nutzer bestätigt anschließend ausdrücklich die Empfehlung zu Nr. 5: Nach Einwandbehandlung und Erklärung einmal menschliche Beratung anbieten. Bei Zustimmung einen Termin vereinbaren, andernfalls freundlich beenden. Die Zustimmung zum Human-Angebot erfüllt den ausdrücklichen Human-Wunsch; die Datenlücke wird offen übergeben. Keine automatische AI-Wiederanrufserie. Eindeutige Aufforderungen, das Gespräch zu beenden oder nicht mehr anzurufen, haben weiterhin sofort Vorrang.

## Alternativen und Folgen

Die Alternative, schon jedes erste „Kein Interesse“ ohne Klärung zu beenden, wurde nicht gewählt. Unbegrenzte Einwandbehandlung und ein pauschaler Drei-Nein-Zähler folgen ebenfalls nicht aus dieser Entscheidung. Der konkrete Vorbehalt und die jeweils letzte Kundenaussage bestimmen den nächsten Schritt.

Ein Kontaktstopp, ein Ende dieses Gesprächs, Zeitmangel und ein Rückrufwunsch müssen getrennt erhalten bleiben. Die Reichweite ist mit Nr. 3A für weitere StepEnergy-Vertriebsanrufe durch AI und Menschen entschieden. Die gemeinsame Backend-Abbildung dieser Sperre bleibt ein Vorschlag für den Supervisor und muss technisch abgesichert werden. Eine Gesprächsbeendigung erzeugt keine automatische Buchung und darf nicht nachträglich zu Interesse umgedeutet werden.

## Umsetzung und gemeinsame Verträge

Betroffen sind insbesondere `PermissionTask`, `NeinArtTask`, `OutcomeTask`, die Abbruchpfade und `_pack_dc_results`. Das bestehende boolesche Permission-Feld reicht zur Abbildung der fachlichen Unterschiede nicht allein aus. Konkrete Zustands- und Wirefelder werden erst spezifiziert; gemeinsame EnergyWarm-Verträge bleiben Vorschläge für den Supervisor.

Keine Produktimplementierung durch dieses ADR. Spätere Korrekturen und Prüfungen folgen ADR-005 in V3; Übernahme ins Original nur im vorgesehenen konkreten Übernahmeauftrag. Empfänger müssen neue Abschlussbedeutungen vor dem Sender verstehen. Ein technischer Rollback darf ausdrücklich festgehaltene Kontaktstopps nicht in Rückrufaufträge umdeuten.
