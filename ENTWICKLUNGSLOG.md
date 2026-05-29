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
