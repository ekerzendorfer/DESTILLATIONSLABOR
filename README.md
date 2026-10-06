# DESTILLATIONSLABOR

**Version:** v0.9.2  
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
