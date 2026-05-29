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
