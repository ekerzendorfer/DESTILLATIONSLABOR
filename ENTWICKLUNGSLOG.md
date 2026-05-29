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

## Phase 5 – Korrekturrunde Version 0.8.2

Ausgangspunkt waren erste Tests von Version 0.8.1 im Browser und im GitHub-Pages-Repo. Dabei wurden mehrere Darstellungs- und Modellierungsprobleme sichtbar, die in Version 0.8.2 gezielt korrigiert wurden.

### Beobachtungen aus dem Test
- Die Legende F1/F2/F3 lag innerhalb der Apparaturgrafik und überdeckte den unteren Bereich der Heizhaube.
- Bei Aceton/Toluol entstand unter mittleren Bedingungen kaum oder keine Mischfraktion; der Übergang war im Modell zu abrupt.
- Bei Methanol/Ethanol entstand unter mittleren Bedingungen eine zu große Mischfraktion.
- Beim Fraktionswechsel schwenkte zwar das Ablaufrohr, die Tropfen fielen aber weiterhin in das erste Auffanggefäß.
- Zwischen Kolonne und Kühler erschien während der Tropfanimation ein störendes dunkles trapezförmiges Element.
- Die eingestellte Anfangszusammensetzung wurde in der Zusammensetzungsanzeige nicht erwartungskonform sichtbar, da die Simulation intern mit Stoffmengenanteilen rechnet, die Anzeige aber didaktisch als Volumenanteil verstanden wurde.

### Änderungen in Version 0.8.2
- Versionskennung im Header auf 0.8.2 geändert.
- Legende F1/F2/F3 aus der Apparaturfläche herausgenommen und als eigene Zeile unter die gesamte Grafik gesetzt.
- Verbindungsschliff zwischen Kolonne und Kühler grafisch entschärft: keine dunkle Füllfläche mehr, nur noch helle Konturzeichnung.
- Tropfenposition korrigiert: Die Tropfenform wird nun beim Fraktionswechsel mit absoluten SVG-Koordinaten neu gesetzt, damit die CSS-Fallanimation die seitliche Position nicht überschreibt.
- Zusammensetzungsanzeige im Kolben auf Volumenanteile umgestellt, damit sie mit dem Startregler übereinstimmt. Die thermodynamische Rechnung verwendet weiterhin Stoffmengenanteile.
- Dampfzusammensetzung am Kopf mit einem einfachen Kolonnen-/Kopf-Holdup geglättet, um unrealistisch abrupte Sprünge zu vermeiden.
- Automatische Fraktionsgrenzen erneut gemischabhängig kalibriert:
  - Aceton/Toluol: Übergangsbereich verbreitert, damit auch bei gut trennbaren Gemischen eine kleine Mischfraktion sichtbar werden kann.
  - Cyclohexan/Toluol: weitgehend beibehalten, da die Testwerte plausibel wirkten.
  - Methanol/Ethanol: Übergangsbereich wieder verkleinert, da Version 0.8.1 eine zu große Mischfraktion erzeugte.
  - Ethylacetat/1-Butanol: eigene Fraktionsgrenzen ergänzt.

### Didaktische Einordnung
- Die App bleibt bewusst ein didaktisch vereinfachtes Modell. Die aktuellen Anpassungen dienen nicht der exakten Prozesssimulation, sondern einer plausibleren und besser interpretierbaren Darstellung des Zusammenhangs von Heizleistung, Kolonnenleistung, Dampfzusammensetzung und Fraktionsbildung.

## Phase 6 – Version 0.8.3: Startkorrektur und bereinigte Kühlergrafik

- Version auf **0.8.3** gesetzt.
- Fehler beim Start der automatischen Fraktionierung korrigiert:
  - Die Kopf-/Dampfzusammensetzung startet beim ersten Sieden nun direkt mit der tatsächlich berechneten Zusammensetzung.
  - Dadurch fällt zu Beginn nicht mehr fälschlich ein kleines Volumen in die Mischfraktion.
- Automatische Fraktionslogik weiter feinjustiert:
  - gemischabhängige Reaktionsgeschwindigkeit des Kopf-/Kolonnen-Holdups eingeführt,
  - Aceton/Toluol bleibt sehr leicht trennbar, soll aber nicht völlig ohne Übergangsbereich wirken,
  - Methanol/Ethanol wurde gegenüber der zu breiten Mischfraktion vorsichtig entschärft,
  - Cyclohexan/Toluol bleibt als plausibler Kalibrier-Anker weitgehend erhalten.
- Kühler-/Verbindungsbereich grafisch bereinigt:
  - der schräge Kühlerkörper wird nicht mehr als halbtransparent gefülltes Polygon, sondern als Glas-Outline gezeichnet,
  - das störende dunkle trapezförmige Artefakt zwischen Kolonne und Kühler sollte damit verschwinden.
- Tropfen-/Fraktionswechsler-Animation aus Version 0.8.2 beibehalten:
  - der Auslassarm zeigt zum aktiven Auffanggefäß,
  - die Tropfen fallen in das aktive Gefäß.
- Zusammensetzungsanzeigen robust gemacht:
  - vor dem Sieden wird für den Dampf eine plausible Gleichgewichtsanzeige berechnet,
  - nach Beginn des Siedens wird die reale simulierte Kopfzusammensetzung angezeigt.
- JavaScript-Syntax geprüft.

### Hinweise für den nächsten Test

Besonders zu prüfen:

1. Ob das schwarze/trapezförmige Artefakt im Kühlerbereich verschwunden ist.
2. Ob beim Start der Destillation kein kleines Volumen mehr fälschlich in der Mischfraktion landet.
3. Ob Aceton/Toluol bei mittlerer Kolonne zumindest eine kleine, aber nicht übertriebene Mischfraktion zeigt.
4. Ob Methanol/Ethanol keine übermäßig große Mischfraktion mehr bildet.
5. Ob Cyclohexan/Toluol weiterhin ungefähr im plausiblen Bereich bleibt.

## Phase 6 – Version 0.8.3 FIX

Korrektur, nachdem die zuvor bereitgestellte 0.8.3 inhaltlich noch auf 0.8.2 stehengeblieben war.

### Fehlerkorrekturen
- Sichtbare Versionskennung auf `Version 0.8.3 FIX` gesetzt.
- Startfehler der automatischen Fraktionierung korrigiert:
  - `lastYA` startet nun als `null` statt als neutraler Wert `0.5`.
  - Beim ersten Sieden wird die Kopfzusammensetzung direkt aus dem berechneten Gleichgewichtswert gesetzt.
  - Aktive Fraktion, Kandidat und Hysterese werden beim ersten Sieden konsistent initialisiert.
  - Dadurch sollte zu Beginn nicht mehr ein kleiner künstlicher Anteil in der Mischfraktion landen.
- Kühlergrafik entschärft:
  - Der schräge Kühlerkörper wird nur noch als Glas-Outline gezeichnet.
  - Das dunkle trapezförmige Artefakt zwischen Kolonne und Kühler sollte dadurch verschwinden.
- Dampfpfad im Kühler optisch schwächer gezeichnet, damit keine dunkle Überlagerung entsteht.
- Fraktionsgrenzen leicht nachkalibriert:
  - Aceton/Toluol: kleine Mischfraktion eher sichtbar.
  - Methanol/Ethanol: Mischfraktion gegenüber der zu breiten 0.8.1 reduziert.
  - Ethylacetat/1-Butanol: Startverhalten stabilisiert.

### Prüfhinweise
- Beim Start der Destillation sollte kein anfänglicher 1-mL-Anteil mehr in der Mischfraktion gesammelt werden.
- Beim Tropfenlauf sollte kein dunkler Trapezbereich mehr zwischen Kolonne und Kühler erscheinen.
- Die Datei ist bewusst als `FIX` gekennzeichnet, um sie sicher von der fehlerhaft bereitgestellten 0.8.3 zu unterscheiden.

## Phase 7 – Version 0.8.4

Stabilisierungsversion auf Basis der funktionierenden Version 0.8.3 FIX. Schwerpunkt: Übergang vom reinen Simulator zum auswertbaren virtuellen Lernlabor.

### Neue Funktionen
- Dynamisches Infoboard unter der Apparatur:
  - erklärt die aktuelle Phase der Destillation sprachlich
  - unterscheidet Aufheizen, Fraktion 1, Mischfraktion, Fraktion 2 und Ende
  - passt Stoffnamen automatisch an das gewählte Gemisch an
- Berechnete Zusammensetzung der Fraktionen:
  - Volumen je Fraktion
  - Zusammensetzung aus Komponente A und B
  - Hauptkomponente und berechnete Reinheit
  - kleine Farbbalken zur schnellen visuellen Erfassung
- Endauswertung nach Abschluss:
  - tabellarische Übersicht über alle Fraktionen
  - berechnete Reinheit je Fraktion
  - einfache Trennqualitätsbewertung mit Sternen
  - Hinweis zur Wirkung von Heizleistung und Kolonnenleistung

### Didaktische Zielsetzung
- Die App soll nicht nur den Ablauf zeigen, sondern den Destillationsprozess erklären.
- Die Fraktionen werden als auswertbare Produkte sichtbar.
- Die Grundlage für spätere virtuelle Messungen wie Dichte, Brechungsindex und Siedebereich ist vorbereitet.

### Noch offen
- Feintuning der absoluten Fraktionsvolumina.
- CSV-Export.
- Virtuelle Messungen der Fraktionen.
- Aufgaben-/Challenge-Modus.

## Phase 8 – Version 0.8.5

Kleine Konsolidierungs- und Plausibilitätsversion. Es wurden bewusst keine neuen Großfeatures ergänzt.

### Änderungen
- Sichtbare Versionskennung auf `Version 0.8.5` gesetzt.
- Interne Startvolumina der beiden Komponenten werden gespeichert (`startVol`).
- Laufende Bilanzprüfung ergänzt:
  - Summe aus Kolbenrest und Fraktionen wird mit dem Startvolumen verglichen.
  - Anzeige als ΔA und ΔB im Infoboard.
  - Kleine Rundungsabweichungen werden toleriert.
- Fraktionsanzeige präzisiert:
  - Gesamtvolumen der Fraktion wird ausdrücklich als Gesamtvolumen angezeigt.
  - Zusammensetzung wird mit einer Nachkommastelle ausgegeben.
  - Zusätzlich werden die enthaltenen Teilvolumina beider Komponenten angezeigt.
  - Dadurch soll verhindert werden, dass Gesamtvolumen und Reinstoffvolumen verwechselt werden.
- Endauswertung präzisiert:
  - Prozentzusammensetzung mit einer Nachkommastelle.
  - Teilvolumina der Komponenten in jeder Fraktion.
- Apparatur leicht verfeinert:
  - Schliffverbindung zwischen Kolben und Kolonne ergänzt.
  - Seitlicher Ansatz für das Sumpfthermometer angedeutet.
  - Auffanggefäße als oben offene Gefäße gezeichnet.
  - Verbindungsschliff am Kühler entfernt/reduziert.

### Noch offen
- Feinkalibrierung der Fraktionsgrenzen, besonders bei Aceton/Toluol.
- Virtuelle Messwerte der Fraktionen.
- CSV-Export.
