# Daten
In diesem Kontext werden Daten als Informationen verstanden, die von externen Quellen geladen werden, genauso wie von intern generierten AgenaScripts stammende Datensätze.

## Balken  (Kerzen)
### Modus Operandi
Ein klassischer Indikator wird einen oder mehrere Wert(e) anhand der verfügbaren Datenreihen berechnen.
Datenreihen in diesem Sinne können aus Schlusspreisen, Tiefs, Stundencharts oder 10-Minutenperioden usw. bestehen. Jede Periode (Kerze) wird einem spezifischen Indikator zugewiesen.

In den folgenden Beispielen und Abbildungen werden wir einen Indikatorwert annehmen, der von etwas wie einem einfachen gleitenden Durchschnitt generiert wird.

Um einen gleitenden Durchschnitt zu berechnen, braucht AgenaTrader eine Datenreihe; hierfür werden wir die Schlusspreise heranziehen. Alle Schlusspreise für die Balken (Kerzen) innerhalb eines Charts werden in einer Liste gespeichert und numerisch geordnet.
Der aktuelle Schlusspreis des aktuellen Balkens wird am rechten Eck des Charts angezeigt und wird die Nummer 0 zugewiesen. Der Balken links davon wird die Nummer 1 zugewiesen, und so weiter. Der älteste abgebildete Balken wird die Nummer 500 haben (als Beispiel).
Wird ein neuer Balken während der aktuellen Handelssession hinzugefügt, wird dieser Balken die Nummer 0 zugewiesen, und der vorangegangene Balken – der bis zu diesem Punkt Balken Nummer 0 war – wird nun neu als Balken 1 eingeordnet werden, und der älte
ste Balken ganz links wird nun die Nummer 501 haben.

Innerhalb eines Scripts (selbsterstelltes Programm) ist das „Close“-Array die Liste aller Schlusspreise. Der letzte Schlusspreis ist daher Close\[0\] und der Schlusspreis davor (Balken links vom letzten Balken) ist Close\[1\] usw., und die älteste Kerze hat dabei den Wert von Close\[501\]. Hier bezeichnet die Nummer innerhalb der eckigen Klammern den Index des Arrays. Der allgemeine Begriff, der in AgenaTrader verwendet wird, ist „barsAgo“.

Zusätzlich wird jeder Balken nicht nur einen Close-Wert haben, sondern auch einen  [*High*](#high), [*Low*](#low), [*Open*](#open), [*Median*](#median), [*Typical*](#typical), [*Weighted*](#weighted), [*Time*](#time) гnd [*Volume*](#volume). Zeitraum wäre der Hoch der Kerze, die vor 10 Perioden aufgetreten ist, High\[10\], der Tief des letzten Tages wäre Low\[1\].

**Wichtiger Hinweis:**
Die oben erwähnten Beispiele betreffen Berechnungen, die am Ende einer Periode ausgeführt werden. Die Werte für die aktuell laufenden und unfertigen Kerzen werden nicht berücksichtigt.

Wenn Sie die Werte der aktuell laufenden und unfertigen Kerzen bekommen möchten, müssen Sie CalculateOnBarClose = falsch einstellen. Wie beim vorigen Beispiel wird der aktuell laufende Balken die Nummer 0 erhalten und so weiter.
Close\[0\] wird Ihnen den aktuellsten Preis, der vom Datenanbieter geliefert wird, liefern. Für alle Werte der Balken High\[0\]...Low\[0\]... etc. sind Änderungen vorbehalten bis der Balken abgeschlossen und ein neuer Balken angefangen wird. Der einzige Wert, der sich auf keinen Fall ändern wird, ist Open\[0\].


## Data Series
### Beschreibung
Datenserien werden in AgenaTrader zum einen unterschieden in die frei für die eigene Programmierung verwendbaren Datenserien zum Speichern von Werten unterschiedlicher Datentypen und zum anderen in die in AgenaTrader fest integrierten Datenserien, die die Kursdaten der einzelnen Bars enthalten. Die letzteren werden hier vorgestellt.
Das Konzept von Datenserien wird sehr konsequent und durchgängig verfolgt. Alle Kursdaten der einzelnen Bars sind in Datenserien organisiert.

Folgende Datenserien sind verfügbar:

[*Open*](#open)

[*High*](#high)

[*Low*](#low)

[*Close*](#close)

[*Median*](#median)

[*Typical*](#typical)

[*Weighted*](#weighted) [*Weighteds*](#weighteds)

[*Time*](#time) [*Times*](#times)

[*TimeFrame*](#timeframe) [*TimeFrames*](#timeframes)

[*Volume*](#volume) [*Volumes*](#volumes)

## Open
### Beschreibung
Open ist eine Datenserie vom Typ Dataseries, in der die historischen Eröffnungskurse gespeichert sind.

### Parameter
barsAgo Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Open
Open[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

### Beispiel
```cs
// Eröffnungskurs der aktuellen Periode
Print(Time[0] + " " + Open[0]);

// Eröffnungskurs des Bars von vor 5 Perioden
Print(Time[5] + " " + Open[5]);


// aktueller Wert für den SMA 14 über die Eröffnungskurse (gerundet)
Print("SMA(14) Calculated using the opening prices: " + Instrument.Round2TickSize(SMA(Open, 14)[0]));
```

## High
### Beschreibung
High ist eine Datenserie vom Typ Dataseries, in der die historischen Höchstkurse gespeichert sind.

### Parameter
barsAgo Indexwert (s. [*Bars*](#bars-candles))

### usage
```cs
High
High[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft  *CalculateOnBarClose*.

### Beispiel
```cs
// Höchstkurs der aktuellen Periode
Print(Time[0] + " " + High[0]);

// Höchstkurs des Bars von vor 5 Perioden
Print(Time[5] + " " + High[5]);

// aktueller Wert für den SMA 14 über die Höchstkurse (gerundet)
Print("SMA(14) calculated using the high values: " + Instrument.Round2TickSize(SMA(High, 14)[0]));
```

## Low
### Beschreibung
Low ist eine Datenserie vom Typ Dataseries, in der die historischen Tiefstkurse gespeichert sind.

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Low
Low[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

### Beispiel
```cs
// Tiefstkurs der aktuellen Periode
Print(Time[0] + " " + Low[0]);

// Tiefstkurs des Bars von vor 5 Perioden
Print(Time[5] + " " + Low[5]);

// aktueller Wert für den SMA 14 über die Tiefstkurse (gerundet)
Print("SMA(14) calculated using the low prices: " + Instrument.Round2TickSize(SMA(Low, 14)[0]));
```

## Close
### Beschreibung
Close ist eine Datenserie vom Typ Dataseries, in der die historischen Schlusskurse gespeichert sind.

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Close
Close[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

Indikatoren werden standardmäßig über die Schlusskurse berechnet. Die Angabe der Input-Serie kann weggelassen werden (siehe Beispiel unten).

### Beispiel
```cs
// Schlusskurs der aktuellen Periode
Print(Time[0] + " " + Close[0]);

// Schlusskurs des Bars von vor 5 Perioden
Print(Time[5] + " " + Close[5]);

// aktueller Wert für den SMA 14 über die Schlusskurse (gerundet)
Print("SMA(14) berechnet über die Schlusskurse: " + Instrument.Round2TickSize(SMA(Close, 14)[0]));

// Close kann auch weggelassen werden, da es per Default verwendet wird.
Print("SMA(14) berechnet über die Schlusskurse: " + Instrument.Round2TickSize(SMA(14)[0]));
```

## Median
### Beschreibung
Median ist eine Datenserie vom Typ Dataseries, in der die historischen Median-Werte gespeichert sind.

Der Median-Preis eines Bars ergibt sich aus (High + Low) / 2.

Siehe auch [*Typical*](#typical) and [*Weighted*](#weighted).

### Parameter
barsAgo Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Median
Median[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft  *CalculateOnBarClose*.

Informationen zu Median, Typical und Weighted:
<http://blog.nobletrading.com/2009/12/median-price-typical-price-weighted.html>

### Beispiel
```cs
// Median-Preis der aktuellen Periode
Print(Time[0] + " " + Median[0]);

// Median-Preis des Bars von vor 5 Perioden
Print(Time[5] + " " + Median[5]);

// aktueller Wert für den SMA 14 über die Median-Preise (gerundet)
Print("SMA(14) berechnet über die Openkurse: " + Instrument.Round2TickSize(SMA(Median, 14)\[0\]));
```

## Typical
### Beschreibung
Typical ist eine Datenserie vom Typ Dataseries, in der die historischen Typical-Werte gespeichert sind.

Der Typical-Preis eines Bars ergibt sich aus (High + Low + Close) / 3.

Siehe auch [*Median*](#median) and [*Weighted*](#weighted).

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Typical
Typical[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft  *CalculateOnBarClose*.

Informationen zu Median, Typical und Weighted:
<http://blog.nobletrading.com/2009/12/median-price-typical-price-weighted.html>

### Beispiel
```cs
// Typical-Preis der aktuellen Periode
Print(Time[0] + " " + Typical[0]);

// Typical-Preis des Bars von vor 5 Perioden
Print(Time[5] + " " + Typical[5]);

// aktueller Wert für den SMA 14 über die Typical-Preise (gerundet)
Print("SMA(14) berechnet über die Openkurse:" + Instrument.Round2TickSize(SMA(Typical, 14)[0]));
```

## Weighted
### Beschreibung
Weighted ist eine Datenserie vom Typ Dataseries, in der die historischen Weighted-Werte gespeichert sind.

Der Weighted-Preis eines Bars ergibt sich aus (High + Low + 2*Close) / 4. (gewichtet auf den Schlusskurs)

Siehe auch [*Median*](#median) & [*Typical*](#typical).

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Weighted
Weighted[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft  *CalculateOnBarClose*.

Informationen zu Median, Typical und Weighted:
<http://blog.nobletrading.com/2009/12/median-price-typical-price-weighted.html>

### Beispiel
```cs
// Weighted-Preis der aktuellen Periode
Print(Time[0] + " " + Weighted[0]);

// Weighted-Preis des Bars von vor 5 Perioden
Print(Time[5] + " " + Weighted[5]);

// aktueller Wert für den SMA 14 über die Weighted-Preise (gerundet)
Print("SMA(14) berechnet über die Openkurse: " + Instrument.Round2TickSize(SMA(Weighted, 14)[0]));
```

## Weighteds
### Beschreibung
Weighteds ist ein Array von  *DataSeries*\[1\] welches alle [*Weighted*](#weighted)-Datenserien enthält.

Dieses Array ist nur in Indikatoren bzw. Strategien von Bedeutung, die Daten aus mehreren Zeiteinheiten verarbeiten.

Ein neuer Eintrag wird dem Array immer dann hinzugefügt, wenn dem Indikator bzw. der Strategie eine neue Zeiteinheit hinzugefügt wird.

Mit **\[TimeFrameRequirements(("1 Day"), ("1 Week"))\]**  enthält das Array 3 Einträge.

*Weighteds*\[0\] die Weighted-Dataseries der Chart-Zeiteinheit
*Weighteds*\[1\] die Weighted-Dataseries aller Bars auf Tagesbasis
*Weighteds*\[2\] die Weighted-Dataseries aller Bars auf Wochenbasis.

*Weighteds*\[0\]\[0\] entspricht *Weighteds*\[0\].

Siehe auch  [*MultiBars*](#multibars).

### Parameter
barsAgo	Indexwert der einzelnen Bars innerhalb der Dataseries
barSeriesIndex Indexwert der unterschiedlichen Zeiteinheiten

### Verwendung
```cs
Weighteds[int barSeriesIndex]
Weighteds[int barSeriesIndex][int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft  *CalculateOnBarClose*.

### Beispiel
Siehe Beispiel unter  [*Multibars*](#multibars).

## Time
### Beschreibung
Time ist eine [*DataSeries*](#dataseries) vom Typ [*DateTimeSeries*](#datetimeseries), in der die Zeitstempel der einzelnen Bars gespeichert sind.

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Time
Time[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

### Beispiel
```cs
// Zeitstempel der aktuellen Periode
Print(Time[0]);
// Zeitstempel des Bars von vor 5 Perioden
Print(Time[5]);
```

## Times
### Beschreibung
Times ist ein Array von *DataSeries* welches alle [*Time*](#time)-Datenserien enthält.

Dieses Array ist nur in Indikatoren bzw. Strategien von Bedeutung, die Daten aus mehreren Zeiteinheiten verarbeiten.

Ein neuer Eintrag wird dem Array immer dann hinzugefügt, wenn dem Indikator bzw. der Strategie eine neue Zeiteinheit hinzugefügt wird..

Mit **\[TimeFrameRequirements(("1 Day"), ("1 Week"))\]** enthält das Array 3 Einträge.

*Times*\[0\] die Time-Dataseries der Chart-Zeiteinheit
*Times*\[1\] die Time-Dataseries aller Bars auf Tagesbasis
*Times*\[2\] die Time-Dataseries aller Bars auf Wochenbasis.

*Times*\[0\]\[0\]  entspricht *Times*\[0\].

Siehe auch [*MultiBars*](#multibars).

### Parameter
barsAgo		Indexwert der einzelnen Bars innerhalb der Dataseries
barSeriesIndex	Indexwert der unterschiedlichen Zeiteinheiten

### Verwendung
```cs
Times[int barSeriesIndex]
Times[int barSeriesIndex][int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

### Beispiel
Siehe Beispiel unter [*Multibars*](#multibars).

## Volume
### Beschreibung
Volume ist eine  [*DataSeries*](#dataseries) vom Typ [*DataSeries*](#dataseries), in der die historischen Umsätze gespeichert sind.

### Parameter
barsAgo	Indexwert (s. [*Bars*](#bars-candles))

### Verwendung
```cs
Volume
Volume[int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

Der vom Indikator  [*VOL()*](#vol) zurückgelieferte Wert ist identisch mit dem hier beschriebenen Volumen.
Z.B. liefert *Vol()*\[3\] den gleichen Wert wie *Volume*\[3\].

### Beispiel
```cs
// Volumen der aktuellen Periode
Print(Time[0] + " " + Volume[0]);
// Volumen des Bars von vor 5 Perioden
Print(Time[5] + " " + Volume[5]);
// aktueller Wert für den SMA 14 über das Volumen (gerundet)
Print("SMA(14) berechnet über das Volumen: " + Instrument.Round2TickSize(SMA(Volume, 14)[0]));
```

## Volumes
### Beschreibung
Volumes ist ein Array von *DataSeries* welches alle [*Volume*](#volume)- Datenserien enthält.
Dieses Array ist nur in Indikatoren bzw. Strategien von Bedeutung, die Daten aus mehreren Zeiteinheiten verarbeiten.

Ein neuer Eintrag wird dem Array immer dann hinzugefügt, wenn dem Indikator bzw. der Strategie eine neue Zeiteinheit hinzugefügt wird.

Mit **\[TimeFrameRequirements(("1 Day"), ("1 Week"))\]**enthält das Array 3 Einträge.

Volumes\[0\] die Volume-Dataseries der Chart-Zeiteinheit
Volumes\[1\] die Volume-Dataseries aller Bars auf Tagesbasis
Volumes\[2\] die Volume-Dataseries aller Bars auf Wochenbasis.

Volumes\[0\]\[0\] entspricht Volumes\[0\].

Siehe auch [*MultiBars*](#multibars).

### Parameter
barsAgo	Indexwert der einzelnen Bars innerhalb der Dataseries

barSeriesIndex Indexwert der unterschiedlichen Zeiteinheiten

### Verwendung
```cs
Volumes[int barSeriesIndex]
Volumes[int barSeriesIndex][int barsAgo]
```

### Weitere Informationen
Der zurückgegebene Wert ist abhängig von der Eigenschaft *CalculateOnBarClose*.

### Beispiel
Siehe Beispiel unter  [*Multibars*](#multibars).

## TimeFrame
### Beschreibung
TimeFrame ist ein Zeitrahmenobjekt.

### Verwendung
```cs
TimeFrame
```

## TimeFrames
### Beschreibung
TimeFrames ist ein Array von TimeFrame-Objekten, welches für jedes Bar-Objekt ein separates TimeFrame-Objekt  enthält.

Dieses Array ist nur in Indikatoren bzw. Strategien von Bedeutung, die Daten aus mehreren Zeiteinheiten verarbeiten.

Ein neuer Eintrag wird dem Array immer dann hinzugefügt, wenn dem Indikator bzw. der Strategie eine neue Zeiteinheit hinzugefügt wird.

Mit **\[TimeFrameRequirements(("1 Day"), ("1 Week"))\]** enthält das Array 3 Einträge.

```cs
TimeFrames [0]; //TimeFrame der primären Datenserie (Chart-Zeiteinheit)
TimeFrames [1];
Print(TimeFrames[1]); // liefert "1 Day"
TimeFrames [2];
Print(TimeFrames[2]); // liefert "1 Week"
```

TimeFrames \[0\] entspricht [*TimeFrame*](#timeframe).

Siehe auch  [*MultiBars*](#multibars).

### Parameter
barSeriesIndex Indexwert der unterschiedlichen Zeiteinheiten

### Verwendung
```cs
TimeFrames [int barSeriesIndex]
```
### Beispiel
```cs
if (ProcessingBarSeriesIndex == 0 && ProcessingBarIndex == 0)
for (int i = BarsArray.Count-1; i >= 0; i--)
Print("The Indicator " + this.Name + " uses Bars of the Timeframe " + TimeFrames[i]);
```
