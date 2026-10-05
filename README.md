# DESTILLATIONSLABOR

**Version:** v0.9.1  
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
