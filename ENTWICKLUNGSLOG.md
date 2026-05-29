# Entwicklungslog: Virtuelle Destillation

## Phase 1 – Konzept
- Ziel: browserbasierte Simulation einer fraktionierenden Destillation für SEK1/SEK2.
- Technischer Rahmen: Single-File-HTML, später auslagerbare JSON-Daten.
- Modell: idealisierte binäre Gemische, Antoine-Gleichung, Raoult/Dalton, vereinfachte Kolonnenwirkung.
- Didaktischer Schwerpunkt: Zusammenhang zwischen Zusammensetzung, Siedetemperatur, Dampfphase und Fraktionierung.

## Phase 2 – Festlegungen für Version 0.8
- Vier Startgemische:
  - Aceton / Toluol
  - Cyclohexan / Toluol
  - Methanol / Ethanol
  - 1-Butanol / Ethylacetat
- Verunreinigungen, insbesondere Wasser, werden bewusst ausgeschlossen.
- Kein Azeotropmodell in Version 0.8.
- Beschleunigter Simulationsablauf.
- Deutsche UI, Internationalisierung für Englisch vorbereiten.
- Gefahrenstoffkennzeichnung einplanen.

## Phase 3 – Erster lauffähiger Prototyp V0.8

- Erste `index.html` erstellt.
- Single-File-HTML mit eingebetteten Stoff- und Gemischdaten.
- Vier kuratierte binäre Gemische integriert:
  - Aceton / Toluol
  - Cyclohexan / Toluol
  - Methanol / Ethanol
  - Ethylacetat / 1-Butanol
- Vereinfachte thermodynamische Engine:
  - Antoine-Gleichung
  - Raoult/Dalton-Näherung
  - vereinfachte Kolonnenanreicherung über theoretische Böden
- Digitale Anzeigen eingebaut:
  - Sumpftemperatur
  - Kopftemperatur
  - Kolbenvolumen
  - Gesamtdestillat
  - Fraktionsvolumina
- Chart.js-Temperaturkurven eingebaut.
- Animierte SVG-Apparatur mit Kolben, Heizhaube, Kolonne, Kühler und Fraktionsgefäßen.
- Automatischer und manueller Fraktionswechsel vorbereitet.
- Deutsch/Englisch-Umschaltung strukturell vorbereitet.
- Gefahrenkennzeichnung über GHS-Kürzel integriert.
- Modell bewusst didaktisch vereinfacht; keine Wasserverunreinigungen, keine Aktivitätskoeffizienten, keine Azeotrope in V0.8.

## Phase 4 – Version 0.8.1: Fraktionslogik, Lesbarkeit und Apparaturvisualisierung

- Version 0.8.1 als überarbeitete `index.html` erstellt.
- Zeitmaßstab auf die praxisnäheren Stufen **5× / 10× / 20×** geändert; Standard nun **10×**.
- Automatischen Fraktionswechsel fachlich verfeinert:
  - Umstellung von groben Standardgrenzen auf gemischabhängige Grenzwerte.
  - Breitere Mischfraktion zur didaktisch plausibleren Darstellung schwieriger Trennungen.
  - Kleine Hysterese eingebaut: automatischer Fraktionswechsel erfolgt erst nach mehreren stabilen Simulationsschritten.
  - Für Methanol/Ethanol zusätzlich reduzierte effektive Kolonnenwirkung, damit die Trennung nicht unrealistisch perfekt wird.
- Zusammensetzungen im Kolben und im Dampf am Kopf werden weiterhin numerisch angezeigt, zusätzlich aber als Farbbalken visualisiert.
- Aktive Sammlung/aktives Auffanggefäß wird zusätzlich textlich angezeigt.
- Temperaturdiagramm erweitert:
  - **Live-Ansicht** zeigt die laufenden letzten Messpunkte.
  - **Gesamtverlauf** zeigt den gesamten gespeicherten Temperaturverlauf.
- Apparaturgrafik weiterentwickelt:
  - Gegenstrom-Kühlung durch Einlass unten und Auslass oben angedeutet.
  - Kurzer Verbindungsschliff zwischen Steigrohr und Kühler ergänzt.
  - Heizhaube zeigt nun eine glühende Heizspirale statt einer einfachen Glühfläche.
  - Fraktionswechsler führt das Ablaufrohr zum aktiven Auffanggefäß.
  - Tropfen fallen in das jeweils aktive Gefäß.
  - Auffanggefäße erhielten angedeutete Skalenstriche.
- Datenstruktur bleibt eingebettet, ist aber weiter auf spätere Auslagerung in JSON vorbereitet.
- Didaktische Zielrichtung bleibt unverändert: halbwegs realistische, aber bewusst vereinfachte Simulation für SEK1/SEK2; keine Wasserverunreinigungen, keine Aktivitätskoeffizienten, keine Azeotrope in Version 0.8.x.

### Hinweise für den nächsten Test

- Besonders testen: Methanol/Ethanol bei 10×, niedriger Heizleistung und guter Kolonne.
- Erwartung: deutlich größere Mischfraktion als in Version 0.8, aber weiterhin sichtbarer Einfluss von Heizleistung und Säulenleistung.
- Prüfen, ob der automatische Fraktionswechsel didaktisch plausibel wirkt oder ob die Schwellenwerte je Gemisch weiter angepasst werden sollen.
- Prüfen, ob die neue Anzeige des Gesamtverlaufs im Temperaturdiagramm für Unterricht/Erklärung ausreichend gut lesbar ist.

# Ergänzung für ENTWICKLUNGSLOG.md – Version 0.8.1

## Phase 4 – Version 0.8.1: Verfeinerung nach erstem Praxistest

Ausgangspunkt war ein erster erfolgreicher Browser- und GitHub-Pages-Test der Version 0.8. Die Simulation lief stabil, zeigte aber bei sehr guten Trennbedingungen teilweise eine zu kleine Mischfraktion. Außerdem wurden mehrere grafische und didaktische Verbesserungen gewünscht.

### Änderungen an Bedienung und Zeitmaßstab
- Zeitmaßstab auf **5× / 10× / 20×** reduziert.
- Standardwert auf **10×** gesetzt, weil die Destillation damit auch bei niedriger Heizleistung noch flott, aber besser beobachtbar läuft.

### Änderungen am automatischen Fraktionswechsel
- Die Automatik verwendet weiterhin die berechnete Dampfzusammensetzung am Kolonnenkopf.
- Die Grenzwerte wurden gegenüber 0.8 verschärft, damit die Mischfraktion sichtbarer wird.
- Für Methanol/Ethanol gelten strengere Grenzen als für leichter trennbare Gemische.
- Eine kleine Hysterese verhindert nervöses Umschalten bei Grenzwerten.
- Ziel: Der Unterschied zwischen kurzer/guter Kolonne und niedriger/mittlerer Heizleistung soll didaktisch klarer herausarbeitbar sein.

### Änderungen an Anzeigen und Diagramm
- Zusammensetzungen von Kolbeninhalt und Kopfdampf werden zusätzlich zu den Prozentzahlen als Farbbalken dargestellt.
- Anzeige der aktuell aktiven Sammlung ergänzt.
- Temperaturdiagramm erhält zwei Modi:
  - **Live-Ansicht** für die laufende Simulation
  - **Gesamtverlauf** zur Betrachtung des ganzen Temperaturprofils

### Grafische Änderungen an der Apparatur
- Kühlwasser als Gegenstrom deutlicher angedeutet: Einlass unten, Auslass oben.
- Verbindungsschliff zwischen Kolonne/Kopf und Kühler ergänzt.
- Heizhaube zeigt nun eine glühende Heizspirale.
- Fraktionswechsler/Ablaufarm zeigt auf das jeweils aktive Auffanggefäß.
- Tropfen fallen optisch in das aktive Auffanggefäß.
- Auffanggefäße haben angedeutete Skalierungen.

### Offene Punkte für spätere Versionen
- Fraktionsauswertung am Ende der Simulation.
- CSV-Export der Temperatur- und Volumendaten.
- Messfunktionen für Siedebereich, Dichte und Brechungsindex der Fraktionen.
- Weitere Verfeinerung der Kolonnenvisualisierung.
- Eventuell Umschaltung zwischen didaktischem und stärker realitätsnahem Modell.
