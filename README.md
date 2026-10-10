# DESTILLATIONSLABOR

**Version:** v0.9.3  
**Status:** bestehender Single-Mode plus optionaler Analytik-Hub-Adapter

## Single-Mode

Der direkte Aufruf ohne Bridge-Parameter bleibt funktional wie bisher: Gemisch, Volumen, Startzusammensetzung, Kolonne, Heizleistung und Fraktionsmodus können frei gewählt werden.

## Analytik-Hub-Modus

Ein Aufruf mit

```text
?bridge=1&run=RUN_...
```

lädt einen Analyseauftrag aus `CHEMIE_ANALYTIK_HUB`.

Für VCÖ-01:

- wird intern das vorhandene Modell `ethylacetate_butanol1` verwendet,
- werden Stoffidentitäten und interne Zusammensetzungen im UI verborgen,
- sind Ausgangsgemisch, Startvolumen und Startzusammensetzung durch die Probe vorgegeben,
- bleiben Kolonnenleistung, Heizleistung und Fraktionsmodus als methodische Entscheidungen offen,
- wird nach jedem abgeschlossenen Run die bestehende 0–5-Sterne-Trennqualität bewertet,
- werden bei schwacher Trennung konkrete Optimierungshinweise gegeben,
- kann ein neuer Run mit verbesserten Parametern gestartet werden,
- wird die Übernahme an den Hub erst ab der im Run vorgegebenen Mindestqualität freigeschaltet (VCÖ-01: 3/5 Sterne).

Ein akzeptierter Run liefert ein `FRACTIONAL_DISTILLATION`-RESULT mit `produced_samples`. F1, F2, F3 und Rückstand erhalten die im tatsächlichen virtuellen Versuch entstandenen Volumina und internen Zusammensetzungen. Diese internen Werte werden im Hub nicht als Lösung angezeigt, stehen aber später z. B. dem GC-Lab zur Verfügung.

Der nichtflüchtige Bestandteil des VCÖ-01-Falls wird im Destillationsmodell nicht in das binäre Dampf-Flüssig-Gleichgewicht einbezogen und dem Rückstand als Analyt zugeordnet.


## v0.9.2 – fester Integrationsschritt

Der Zeitmaßstab 5× / 10× / 20× beeinflusst nur noch die Darstellungsgeschwindigkeit. Die numerische Destillationsrechnung verwendet unabhängig davon einen festen internen Zeitschritt von 0,05 min.

Damit bleiben bei identischer Kolonne, Heizleistung und Fraktionsführung insbesondere erhalten:

- Fraktionsvolumina,
- interne Fraktionszusammensetzungen,
- automatische Fraktionswechsel,
- Trennqualitätsbewertung.

Die mittlere Fraktion wird in der Oberfläche nun als **Übergangsfraktion** bezeichnet. Sie ist der beim Wechsel zwischen den Hauptfraktionen gesammelte Bereich und muss bei sehr guter Trennung weder groß noch annähernd 50:50 zusammengesetzt sein.

Diese Änderung ist besonders für die Kopplung an GC-LAB wichtig: Das Chromatogramm soll die tatsächlich simulierte Fraktionszusammensetzung abbilden und darf nicht vom gewählten Zeitmaßstab der Destillationsdarstellung abhängen.


## v0.9.3 – graduelleres Kolonnen- und Fraktionsmodell

Nach dem ersten vollständigen VCÖ-01-End-to-End-Lauf wurde das physikalisch-chemische Modell der fraktionierenden Destillation überarbeitet.

### Kolonnenleistung

Die Auswahlwerte 0 / 2 / 5 / 10 werden nicht mehr direkt als ganze ideale Gleichgewichtsstufen interpretiert. Stattdessen verwendet das Modell eine graduelle interne Trennleistung:

- einfache Destillation: 0,0 zusätzliche Gleichgewichtsstufen
- kurze Kolonne: 0,8
- mittlere Kolonne: 1,6
- gute Kolonne: 2,8

Die Heizleistung skaliert diese effektive Stufenzahl kontinuierlich. Mittlere und hohe Heizleistung reduzieren die Trennwirkung stärker als bisher.

Auch Teilstufen werden berücksichtigt: Bei einer nicht-ganzzahligen effektiven Stufenzahl wird zwischen dem aktuellen und dem nächsten Gleichgewichtszustand interpoliert. Dadurch entfallen die früheren sprunghaften Effekte durch ganzzahliges Runden.

### Gleichgewichtsstufen

Jeder idealisierte Gleichgewichtskontakt verwendet den Blasenpunkt der jeweils kondensierten Flüssigkeitszusammensetzung. Die einfache Destillation basiert direkt auf Raoult-/Antoine-Gleichgewicht; der frühere zusätzliche künstliche `simpleBoost` entfällt.

### Kopf-Holdup

Die zeitliche Verzögerung am Kolonnenkopf wird nun als kleine durchströmte Flüssigkeitsmenge modelliert. Die Kopfzusammensetzung reagiert daher auf den tatsächlich pro Integrationsschritt übergehenden Volumenstrom und nicht mehr auf einen frei gewählten Glättungsfaktor.

Interne Holdup-Volumina:
- einfache Destillation: 0,20 mL
- kurze Kolonne: 0,30 mL
- mittlere Kolonne: 0,40 mL
- gute Kolonne: 0,55 mL

### Automatische Fraktionsschnitte

Die Grenzwerte beziehen sich weiterhin auf die Zusammensetzung am Kolonnenkopf, werden aber nicht mehr abhängig von Kolonne oder Heizleistung verschoben. Die Apparatur beeinflusst damit die Trennung; das Qualitätskriterium für den Fraktionswechsel bleibt konstant.

Für Ethylacetat / 1-Butanol beginnt die Übergangsfraktion nun etwas früher (`high = 0.88` statt 0.86).

### VCÖ-01 Referenzverhalten

Für 100 mL Ausgangsgemisch mit 75 Vol-% Ethylacetat / 25 Vol-% 1-Butanol ergibt das Modell bei mittlerer Heizleistung ungefähr folgende Staffelung:

| Kolonne | Übergangsfraktion F2 | typische Bewertung |
|---|---:|---:|
| einfache Destillation | ca. 45 mL | 2★ |
| kurze Kolonne | ca. 23–27 mL | 3★ |
| mittlere Kolonne | ca. 10–12 mL | 4★ |
| gute Kolonne | ca. 3–4 mL | 5★ |

Bei mittlerer Kolonne / mittlerer Heizleistung beginnt der automatische Wechsel F1 → F2 deutlich vor dem früheren nahezu vollständigen Übergang zum 1-Butanol-Siedebereich. Die Übergangsfraktion bleibt klein genug, um eine gute Trennung zu zeigen, ist aber didaktisch und analytisch sichtbar.

Die numerische Integration bleibt unabhängig vom gewählten Darstellungs-Zeitmaßstab.
