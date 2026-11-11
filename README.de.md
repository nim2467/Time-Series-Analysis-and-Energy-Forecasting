# Zeitreihenanalyse und Energiebedarfsprognose

[English](README.md) | [**Deutsch**](README.de.md)

## Projektübersicht

Dieses Projekt untersucht zwei Zeitreihenaufgaben:

1. **Analyse täglicher Schrittzahlen:** Explorative Analyse von 61 Tagesbeobachtungen aus März und April 2026, einschließlich deskriptiver Statistik, Wochentagsmustern, Autokorrelation und STL-Zerlegung.
2. **Prognose des Energiebedarfs eines Microgrids:** Untersuchung und stündliche Vorhersage der Zielgröße `load_demand` mit Holt-Winters, SARIMA und Prophet.

**Ziel:** Zeitliche Strukturen untersuchen und klassische Prognoseverfahren auf einem gemeinsamen chronologischen Testzeitraum vergleichen.


## Methodik

1. **Explorative Schrittzahlanalyse:** Tagesstatistiken, Ausreißer, Wochentagseffekte, Lag-Beziehungen, Autokorrelation, rollierende Statistiken, Stationarität und Saisonalität untersuchen
2. **Aufbereitung der Energiedaten:** 15-Minuten-Messwerte laden und numerische Variablen zu stündlichen Mittelwerten aggregieren
3. **Explorative Analyse:** Stündliche Muster, ACF/PACF, STL-Zerlegung und Augmented-Dickey-Fuller-Test untersuchen
4. **Chronologische Aufteilung:** Die ersten 80 % der Stundenwerte als Trainingsdaten und die letzten 20 % (290 Stundenwerte) als Testdaten verwenden
5. **Prognosemodelle:** Additives Holt-Winters-Modell mit Tagesperiodik, SARIMA `(1,1,1) × (1,0,1,24)` und Prophet mit Tages- und Wochenperiodik
6. **Bewertung:** MAE, MSE und RMSE auf demselben Testzeitraum vergleichen und Residuen analysieren


## Ergebnisse

Die folgenden Kennzahlen stammen aus **gespeicherten Notebook-Ausgaben** und wurden für das Portfolio nicht unabhängig neu berechnet. Sie beziehen sich auf den zurückgehaltenen stündlichen Testdatensatz zum Energiebedarf.

| Modell | Test-MAE | Test-MSE | Test-RMSE |
|---|---:|---:|---:|
| Holt-Winters | 84,3449 | 11193,4492 | 105,7991 |
| SARIMA | 84,3087 | **11024,6266** | **104,9982** |
| Prophet | **83,8774** | 11027,3574 | 105,0112 |

**Vergleich:** SARIMA erzielte den geringsten Test-RMSE, Prophet den geringsten MAE. Die Unterschiede sind sehr klein. Eine einzelne Testaufteilung belegt noch keine generelle Überlegenheit eines Modells.

## Interpretation und Einschränkungen

- Die persönliche Schrittzahlreihe ist mit 61 Tagen kurz und nicht auf andere Personen übertragbar; die Messung hängt davon ab, ob das Telefon mitgeführt wurde.
- Die Microgrid-Modelle wurden auf einer einzigen chronologischen 80/20-Aufteilung verglichen, ohne Walk-forward-Validierung oder externe Validierung.
- Die Energieprognosen sind **univariat**: Es werden keine zusätzlichen erklärenden Variablen in die Prognosemodelle einbezogen.
- Modellbewertungen sollten mehrere Kennzahlen und zeitlich korrekte Validierung berücksichtigen.
- Gespeicherte Notebook-Ausgaben wurden für die Portfolio-Version entfernt; die hier dokumentierten Kennzahlen wurden aus den ursprünglichen Ergebnissen übernommen.
