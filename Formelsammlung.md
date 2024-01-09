# Schaltungstechnik Zusammenfassung

## 0.Klausuraufgaben

1. Übertragungssystem (mit oder ohne Gedächnis)
   - Auftrittswahrscheinlichkeit Y berechnen
   - Entropie der Quelle
   - Matrix der Bedingten Wahrscheinlichkeiten
  - Verbundentropie als funktion der Wahrscheinlichkeit

2. Automaten
   - Zustandsfolgediagramm
   - Inverser Automat
   - Speicherzahl
   - Erklarung Automat
   - Automatentafel
   - Wahrscheinlichkeit aller Zustande
   - Trellis-Diagramm

3. PDF
    - Konstante Bestimmen
    - Quantisierung->  Stufenhohe
    - ...
   


## 1. Übertragungssysteme
-Stochastik Basics (Kapitel 2)


### Blockschaltbilder

> |Block|Beschreibung|
>|----------|---------|
>|T|Verzögerungsglied|
>|=1|XOR|
>|&|AND|
>|x(k)|Eingang|
>|y(k)|Ausgang|
>
>
>**XOR Formel**
>$$ y(k) =  x_1(k)*\overline{x_2(k)}+ x_2(k)*\overline{x_1(k)}$$
>
>**AND Formel**
>$$ y(k) =  x_1(k)*x_2(k)$$
>**OR Formel**
>$$ y(k) =  x_1(k)+x_2(k)$$
>
>
>**Ausgabe Berechnen**
bsp. prob(x(k)=1)=q=0.75 
> |x(k)|x(k-1)|...|x(k-n)|y<sub>1</sub>(k)|y<sub>2</sub>(k)|P|
>|---|---|---|---|---|---|---|
>|0|0|-|0|||(1-q)³|
>|0|0|-|1|||(1-q)²*q|
>|0|1|-|0|||(1-q)²*q|
>|0|1|-|1|||(1-q)*q²|
>|...|...|...|...|







### Wahrscheinlichkeiten

> $$P(A|B) = P(A,B)/P(B) $$ Bedingte Wahrschenilichkeit
> Wahrscheinlichkeit von B unter der BEdingung, dass A bereits
> eingetreten ist.

> P(A,B) = Verbundwahrscheinlichkeit
> Wahrscheinlichkeit, dass A und B eintreten

### PDF: Wahrscheinlichkeitsdichtefunktion

> > $$ p(x)=\frac{d}{dx}P(x) $$ 
> CDF Monoton Wachsend

### CDF: Verteilungsfunktion:

> $$ P(x) = \int_{-\infty}^{x} p(u)  \, du $$
> Wertebereich von 0 bis 1
 




### Entropie

>Ergebnis in Bit/Zeichen
> $$ H(x) = - \sum_{i=1}^{q}P(x_{i})*log_{N}(P(x_{i})
) $$

### Informationsgehalt
> $$ I(x_{i})=-log_{N}(P(x_{i})) $$ 


## 2. Automatentheorie

### Finite State Maschine

Fünf Charakterisierende Eigenschaften
|Variabel|Beschreibung|
|----------|---------|
|X<sup>n</sup>|Eingangsgrößen|
|Y<sup>n+1</sup>|Ausgangsgrößen|
|Z<sup>n</sup>|Zustände|
|f<sub>n</sub>|Zustandsfunktion|
|f<sub>a</sub>|Ausgangsfunktion|
|Q|Ausgangsgröße Speicher|


> **Benötigte Speichergröße**
> FSM: Deterministisch Endlicher Automat -> Anzahl Zustände
> Nichtdeterministisch Endlicher Automat -> Anzahl Zustände + Anzahl Eingabesymbole

### Zustandsfolgediagramm

![Zustandsfolgediagramm siehe Skript](/Zustandsfolgediagramm.png)

### Automatentafel

|Zustand|Folgezustand x=0|Folgezustand x=1
|---|---|---|
|Z|Q<sub>0,</sub>,Q<sub>1,</sub>|Q<sub>0,</sub>,Q<sub>1,</sub>|
|---|---|---|
|Z<sub>1,</sub>|Z<sub>0,</sub>|Z<sub>0,</sub>||
|Z<sub>4,</sub>|Z<sub>0,</sub>|Z<sub>0,</sub>||

## 3. Quantisierung und Codierung
-Quellencodierung (Kap5)

|Variabel|Beschreibung
|---|---|
|N|Anzahl Codewörter|
|q|Anzahl Elementarzeichen, binär=2|
|n|Codewortlange|

Bei fester Codewortlänge gilt
$$ n=q^n $$

Notwendige Codewortlänge
$$ n=log_q(N) $$ auf ganze Zahlen Aufrunden!

mittlere Codewortlange
$$ \bar{n}=\sum_{i=1}^{N}P(c_{i})*n(c_i) $$
also summe Auftritswahrscheinlichkeit*Länge des Codeworts

Coderedundanz

$$ R_C = \bar{n}-H $$

relative Coderedundanz
$$ r_C = 1-\frac{H}{\bar{n}} $$

Ein Code ist dann und nur dann eindeutig decodierbar, wenn kein Codewort linker Teil eines
anderen Codewortes (Prefix) ist.

dann folgt $H(x) <= n < H(X)+1$
Fano Code...
Huffman Code (Meist besser als Fano)

Lempel-Ziv-Welch-Algorithmus

### Quantisierung

|Variabel|Beschreibung|
|---|---|
|$x$ |Inputbereich|
|$\hat{x_i}$ |Stufenhöhe/Zeichen|
|$i$ |Anzahl Stufen|
|$\Delta$ |Stufenhöhe|



#### Quantisierungsstufen $\Delta$
>$$ \Delta = \frac{x_{max}-x_{¬min}}{i} $$

**Quantisierungsintervalle nach P($x_i$)**
für Symmetrische Codierung
>$$\int_{0}^{x_i}p(x)dx=w; mit w =Wahrscheinlichkeit/AnzahlStufen$$



Quantisierungsfehler 
> $$e(k) = x(k)-s(nT)$$



### Codierung

**Fano-Shannon-Codierung**
1. Ordnen aller Primärzeichen nach fallender Wahrscheinlichkeit.
2. Aufteilen aller Zeichen in zwei Gruppen derart, dass beide Gruppen etwa die gleiche
Summenwahrscheinlichkeit haben.
3. Nun werden die beiden Gruppen codiert, z. B. die obere Gruppe mittels einer „0“ und die
untere Gruppe mittels einer „1“.
4. Die einzelnen Gruppen werden nun analog zu Schritt 2 weiter in gleich wahrscheinliche
Gruppen unter Beibehaltung der Reihenfolge aufgeteilt und entsprechend oben mit einer
„0“ und unten mit einer „1“ codiert.
5. Der Schritt 4 wird so lange angewendet, bis keine weitere Gruppeneinteilung mehr mög-
lich ist

![Fano Codierung siehe Skript](/Fano-Baum.png)

### Kanalcodierung

|Variabel|Beschreibung|
|---|---|
|$$d_{min}$$ |minimale Hammingdistanz (Abstand)|
|$$e_d$$ |Erkennbare Bitumwandlung|
|$$e_c$$ |Korrigierbare BitumwandPlung |
|$$k$$|Datenstellen|
|$$n$$|Codewortstellen|
|$$m$$|Kontrollstellen|
|$$Z$$|Anzahl Codewörter je Kugel|
|$$w$$|Anzahl einsen|
|$$\vec{e}$$| Fehlervektor|
|$$\vec{c}$$| Codevektor|
|$$\vec{c_r}$$| Codevektor recived|
|$$\vec{E}$$| Einheitsmatrix|
|$$\vec{P}$$| Parity Matrix|
|$$\vec{G}$$| Generatormatrix|
|$$\vec{H^{T}}$$| Ḱontrollmatrix|
|$$\vec{S}$$| Syndrom (Fehler)|







>$$ d_{min} = e_d-1 $$
>$$ d_{min} = 2*e_c+1 $$


### Blockcode

Die Generatormatrix $\vec{G}$ ist definiert durch 
>$$ 
>\vec{G}=\begin{bmatrix}
>\vec{P} |&\vec{E}\\
>\end{bmatrix}
>= \begin{bmatrix}
>P_{11} & P_{12} & ... & 1 & 0 & 0 & 0\\
>P_{21} & P_{22} & ... & 0 & 1 & 0 & 0\\
>P_{31} & P_{32} & ... & 0 & 0 & 1 & 0\\
>P_{41} & P_{42} & ... & 0 & 0 & 0 & 1\\
>\end{bmatrix}$$

Die Kontrollmatrix $\vec{H}$ ist definiert durch :

>$$
>\vec{H}=\begin{bmatrix}
>\vec{E} |&\vec{P}\\
>\end{bmatrix}
>$$

Damit gibt sich der Praktische Zusammenhang

>$$\vec{G}*\vec{H} = \vec{0}$$

warum das ganze?
Einfache Fehlererkennung und Berechnung mit:
>mit $$ \vec{c_r}=\vec{c} +\vec{e}$$
>gilt
>$$\vec{S} = \vec{c_r}*\vec{H^{T}} = (\vec{c}+\vec{e})*\vec{H^{T}} =
\vec{c}*\vec{H^{T}}+\vec{e} *\vec{H^{T}} = \vec{e} *\vec{H^{T}}$$
