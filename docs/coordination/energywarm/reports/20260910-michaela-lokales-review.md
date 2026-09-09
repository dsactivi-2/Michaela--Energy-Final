# Lokales Review: Michaela-Spezifikation und Übergabe

Branch: `codex/michaela-specification`, Basis: `main` bei
`99de8d766f6af275a04c7c8eae652a801b8a366b`.
Auf ausdrücklichen Wunsch nur lokal; kein GitHub-PR, kein Push, kein Remote-Setup.

## Problem und Ergebnis

Die bestätigten Gesprächsentscheidungen benötigen einen überprüfbaren
Umsetzungsplan. Dieses Dokumentationspaket verbindet die Fachentscheidungen mit
22 Anforderungen, 44 Situationspfaden, 47 Abnahmekriterien und acht klar
gekennzeichneten Supervisor-Vertragsvorschlägen. Ein Startprompt bereitet eine
neue Sitzung für das Spezifikationsreview und das erste Umsetzungspaket im
Originalprojekt vor. Der Nutzer hat den aktuellen Auftrag auf das normale
Projekt `Livekit agent`, ohne V3, präzisiert.

Einstieg: [Spezifikation](20260909-michaela-spezifikation.md).
Übergabe: [Startprompt](20260910-michaela-naechste-sitzung.md).

## Umfang

Enthalten sind Spezifikation, Matrix, Vertragsvorschläge, technischer Nachweis,
die dafür relevanten vorhandenen Fach-ADRs/Workshop-/Vergleichsdokumente und
lokale Prüfnachweise. Die Quellen wurden hinsichtlich ihres zeitlichen Stands
eingeordnet; historische Berichte bleiben unverändert.

Nicht enthalten sind die bereits vorher vorhandenen Änderungen an Produktcode,
Dependency-Manifesten, Konfiguration und Produkttests. Diese bleiben im lokalen
Arbeitsbaum erhalten. Die dokumentierten 79/132 Tests beziehen sich auf die
im Nachweis bezeichneten tatsächlichen Arbeitsdateien einschließlich vorhandener
Änderungen, nicht auf einen behaupteten identischen HEAD des Dokumentationsbranches.

Einige Quellenverweise zeigen bewusst auf die vorhandenen lokalen Supervisor-/V3-
Ordner oder ältere lokale Auditpakete. Dieses lokale Review publiziert keine
gemeinsamen Verträge und keine vollständige Kopie dieser anderen Arbeitsbereiche.

## Validierung und Grenzen

- Bestehende Offline-Suites im dokumentierten Lauf: Original 79, V3 132 bestanden.
- Produktbereiche: Ruff und Format bestanden; gesamtes Repo hat historische
  I001-/UP017-/Formatbefunde in einer unveränderten Auditdatei.
- Spezifikationsprüfung: 22 R-, 44 M-, 47 AC- und 8 SV-IDs, lokale Verweise und
  Erhalt der erfassten Produktdateien; Einzelheiten im Evidenzverzeichnis.
- Keine Produktimplementierung, keine fachliche Gesamtabnahme vorweggenommen,
  keine neue gemeinsame Vertragsrevision und keine realen Integrationsnachweise.

Der archivierte `20260909-agent-comparison-evidence/source.diff` enthält die
für ein Unified-Diff normalen Leerzeichen auf leeren Kontextzeilen. Ein pauschales
`git diff --check` meldet sie als Whitespace; der historische Nachweis bleibt
bytegleich. Der Commit-Whitespacecheck prüft die übrigen Dateien getrennt,
während das archivierte Diff als Patchformat geprüft wird.

Für das Review sind besonders die Trennung Erlaubnis/Interesse/Rückruf,
vollständige ungebuchte Endpfade, sichere Buchungsbestätigung und Recovery zu
prüfen. Der nächste Schritt ist die Vorbereitung eines konkreten Umsetzungspakets
im Originalprojekt gemäß der aktuellen Nutzerklarstellung. Die historischen
V3-Vergleiche bleiben Nachweise; dieser Auftrag setzt den separaten
Supervisor-Workerablauf unter ADR-005 nicht fort.
