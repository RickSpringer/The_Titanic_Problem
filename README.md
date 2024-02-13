# The_Titanic_Problem

## 1. Einleitung

### 1.1 Datengrundlage & Fragestellung
Das Projekt, 'The Titanic Problem', ermittelt mithilfe verschiedener Datenanlyse-Methoden Indikatoren, die einen Einfluss auf das Überleben der einzelnen Passagiere hatten. Die Faktoren werden in einem zusammengefassten Jupyter Notebook ("The Titanic Problem Notebook") ermittelt und ihr Einfluss mit einfachen Plots illustriert. Als Datensatz wurde der Datensatz "titanic.csv" bereitgestellt.

Als erstes wurden kurze Reports erstellt, um die Eigenschaften der Daten kennenzulernen. Hier wurde nach numerischen und kategorischen Daten gefragt und ob es fehlende Werte gibt. Dies wurde unter Punkt 1.2 im Notebook durchgeführt. Unter "2. Datenerfassung - 2.1 Beobachtungen" wurde genauer auf die bereitgestellten Daten, das Format, Typ und Ähnliches geschaut und eingegangen. Alle Beobachtungen aus dem Datensatz und den Reports aus 1.2 wurden hier als MarkDown festgehalten.

### 1.2 Module, Methoden & Bedingungen
Zur Ausführung des Projekt-Notebooks werden folgende Module in Python benötigt:
- Jupyter 1.0
- Numpy 1.26.4
- Pandas 2.2.0
- Matplotlib 3.8.2

Um die Analyse der Indiatoren durchzuführen zu können, wird der Datensatz zunächst so formatiert, dass Informationen schneller gefiltert werden können und ihr Einfluss gemessen werden kann. Die Datenbereinigung und die konkreten Schritte werden unter Punkt 2.2 "Datenbereinigung" aufgeführt. Nach der Bereinigung werden einzelne Informationen mit der Spalte "Survived" ins Verhältnis gesetzt und aggregiert, wie viele Passagiere mit dem jeweiligen Merkmal absolut und anteilig überlebt haben.

## 2. Datenerfassung & Bereinigung
### 2.1 Beobachtungen
Der Datensatz umfasst *12 Spalten* und 891 Zeilen mit Informationen zu Passagieren der Titanic. Anbei eine Übersicht der Spalten und der hinterlegten Informationen:
**1. 'PassengerId'** Enthält die PassagierId als Integer. Die hinterlegten Zahlen stehen für die IDs und reichen von 1 - 891.

**2. 'Survived'**
Enthält den Überlebensstatus als Integer. 0 = hat nicht überlebt. 1 = hat überlebt.
 
**3. 'Pclass'**
Enthält die Passagierklasse als Integer. Die Zahlen der unterschiedlichen Klassen reichen von 1 - 3.
Frage: Wo genau lagen die Kabinen der Klassen auf dem Schiff? Sind sie etwa Etagen zugeordnet? Wie ist der Zusammenhang zwischen Pclass und Parch?
  
**4. 'Name'**
Enthält die nachfolgenden Informationen als String in der Reihenfolge:

*a. {Nachname} = Nachnamen. Wird in neue Spalte **'Surname'** ausgegliedert. Die Nachnamen werden in eine eigene Spalte {Surname} extrahiert, um später einfacher an Anreden/ Titel zu gelangen. Die Nachname  liegen als einfache Strings vor, z.B. 'Braund', 'Cumings' ...*

*b.  ',' = konstanter Separator nach 'Surname'*

*c.  {Anrede/ Titel} = Titel oder Anreden. Wird in neue Spalte **'Address'** ausgegliedert.*

*d.  Enthält verschiedene Titel und Anreden ('Mr', 'Mrs', 'Miss', 'Master', 'Don', 'Rev', 'Dr', 'Mme', 'Ms', 'Major', 'Lady', 'Sir', 'Mlle', 'Col', 'Capt', 'the Countess', 'Jonkheer').

*e.  '.' = konstanter Separator nach 'Address'*

*f.  {Vornamen} = ein oder mehrere Vornamen. Wird in neue Spalte **'First Name'** ausgegliedert. Die einzelnen Vornamen sind durch ' ' getrennt. Wenn 'Address' nicht 'Miss' ist, werden zuerst die Vornamen des Ehemanns angegeben.*

*g.  {Mädchenname} = Mädchenname. Wird in neue Spalte **'Maiden Name'** ausgegliedert. Wenn Titel/Anrede 'Mrs' ist, wird am Ende der Mädchenname in Klammern angegeben, z.B. (Florence Briggs Thayer). Spitznamen sind teilweise in Anführungszeichen angegeben, z.B. "Frankie"*
                                                                        
**5. 'Sex'**
Enthält das Geschlecht des Passagiers als String. Entweder 'female' für weiblich oder 'male' für männlich.

**6. 'Age'**
Enthält das Alter des Passagiers in Jahren als Float. Die Altersangaben, bsp. von Kindern unter einem Jahr, deuten darauf, dass bei der Datengenerierungen Berechnungen abgelaufen sind, die Floats mit bis zu zwei Nachkommastellen produziert habem. Wie diese Berechnung ablief, ist nicht zu rekonstruieren.

**7. 'SibSp'**
Enthält die Anzahl der Geschwister und/oder der Ehepartner als Integer.

**8. 'Parch'**
Enthält die Anzahl der Elternteile und/oder der Kinder als Integer. Die Werte reichen von 0 - 3.

**9. 'Ticket'**
Enthält Ticketnamen als String. Diese Bezeichnungen setzten sich entweder nur aus Zahlen, aus einer Buchstabenfolge und Zahlen oder einer Kombination aus Sonderzeichen, Buchstaben und Zahlen.

**10. 'Fare'**
Enthält den Ticketpreis als Float mit 4 Nachkommastellen. Die Währung ist nicht angegeben.

**11. 'Cabin'**
Enthält den Namen der Kabine des Passagiers als String. Setzt sich zusammen aus Buchstaben und Zahlenfolge, bsp. 'C85', 'E46'. Insgesamt gibt es 8 verschiedene Kabinentypen. Die Bezeichnung folgt ihren Deckpositionen. So waren die A-Kabinen auf dem obersten Deck und die G-Kabinen auf dem untersten.

**12 'Embarked'**
Enthält den Ort, an dem der Passagier zugestiegen ist als String. S = Southampton (England), C = Cherbourg (Frankreich), Q = Queenstown (Irland).

# 3. Datenbereinigung
Im Ramen der Datenbereinigung wurden alle Daten innerhalb des Datensatzes so formatiert, dass sie anschließend für Berechnungen und Aggregation genutzt werden können. Im Folgenden werden die einzelnen Arbeitsschritte kurz kommentiert.

## 3.1 Formatierung der Namensspalte 'Name'
### 3.1.1
In einem ersten Schritt wurde die Spalte "Name", die im Ursprungsdatensatz die Informationen zur Anrede, Nachname, Vornamen und Mädchenname enthalten hat, in 4 einzelne Spalten aufgeteilt. Hier hat sich herausgestellt, dass bei Eintrag 759 (PassengerId 760) durch den Adelstitel ein Problem für die weitere Analyse entstand, weshalb der Name geringfügig abgeändert werden musste.

### 3.1.2
Mithilfe von split() werden die Nachnamen vom Rest der Namesspalte abgetrennt und in eine eigene Spalte "Surname" ausgegliedert.

### 3.1.3
Anschließend wurde die Anreden/ Titel ebenfalls mit split() von den restlichen Namen abgetrennt. Die Anreden wurden folglich zusammen in der Spalte "Address" und die Vornamen in der Spalte "First Name" geführt.

### 3.1.4
Zuletzt wurde mit extract() der Mädchenname aus der Namensspalte extrahiert und in eine neie Spalte "Maiden Name" ausgegliedert.

## 3.2 Ergänzung der Spalte "Fam"
Um den Einfluss von mitreisenden Familienmitgliedern insgesamt bewerten zu können, wurden die Personen aus der Spalte "SibSp" und "Parch" zusammen in der Spalte "Fam" zusammengefasst und mit 1 addiert. Die Zahl 1 steht hier für den jeweiligen Passagier.

## 3.3 Aufteilung der Kabinen nach Decks
Ausgehend davon, dass sich die Kabinennamen aus einem Buchstaben, der auf das jeweilige Deck schließen lässt, und einer Zahlenfolge zusammmensetzen, wurden die Buchstaben in eine Extraspalte "Cabin_Loc" extrahiert. Da hier nur insgesamt 204 von 891 möglichen Angaben vorhanden waren, wurden die Nullwerte durch ein "N" ersetzt, um sie trotzdem in eine anschließende Analyse mitaufzunehmen.
# Bild Deckaufteilung Titanic!!!

# 4 Datenanalyse
Um den Umfang der Datenanalyse innerhalb der Projektzeit auf ein zu bewältigendes Maß zu begrenzen, wurden folgende Aspekte tiefergehend betrachtet und Diagramme zur Veranschaulichung erstellt:
1. Allgemeine Überlebensrate
2. Überlebensrate nach Passagierklasse und Kabine
3. Überlebensrate nach geschlecht
4. Überlebensrate nach Alter
5. Überlebensrate von Passagieren mit Angehörigen

## 4.1 Allgemeine Überlebensrate
Die Überlebesrate alle Passagiere des Datensatzes gibt einen ersten Eindruck von dem Verhältnis zwischen überlebeneden und verstorbenen Passagieren. Sie wird anhand der "Survived"-Spalte mit der mean() Funktion berechnet und auf zwei Nachkommastellen aufgerundet. Um das Zahlenmäßige Verhältnis zu illustrieren, wurde ein einfaches Diagramm der Anzahl von Überlebenden und Verstorbenen mithilfe der plot-Methode erstellt.

## 4.2 Überlebensrate nach Passagierklasse und Kabine
### 4.2.1 Überlebensrate nach Passagierklasse ("Pclass")
Es wurden die Passagierklassen und Kabinen auf ihren Einfluss auf die Überlebensrate hin überprüft. Zuerst wurde eine Übersicht der Passagierklassenverteilung erstellt und anschließend mit der Spalte "Survived" ins Verhältnis gesetzt. Die Überlebensrate nach Klasse wurde anteilig als Tortendiagramm visualisiert. Zur Formatierung der Darstellung wurden neben der plot-Methode auch Subplots aus dem Matplotlib-Modul genutzt. Anschließend wurde die Überlebensrate absolut als Dezimalzahl für alle drei Klassen ausgedruckt.

### 4.2.1 Überlebensrate nach Kabine ("Cabin_Loc")
Die auf die Decks deutenden Buchstaben der Kabinennamen ("Cabin") wurden nun mit der "Survived"-Spalte abgeglichen und es wurden Anzahlen und Mittelwerte gebildet. Durch die unzureichenden Kabinenangaben, lassen sich keine fundierten Aussagen zum Einfluss der Kabinenposition auf den jeweiligen Decks auf die Überlebenswahrscheinlichkeit treffen. Es fällt aber auf, dass insbeondere die durch "N" ersetzten fehlenden Werte eine besonders niedrige Überlebenswahrscheinlichkeit hatten.  

## 4.3 Überlebensrate nach Geschlecht
Mit der groupby-Funktion wurden die beiden Geschlechter aus der Spalte "Sex" und die Überlebensangaben aus der Spalte "Survived" verglichen. Das daraus resultierende Tortendiagramm zeigt, dass etwa 75% aller Frauen das Unglück überlebt haben. Dagegen waren es bei den Männern nur knapp 20 %. Die Korrelation zwischen dem Geschlecht und der Überlebenswahrscheinlichkeit ist damit deutlich positiv.

## 4.4 Überlebensrate nach Alter
### 4.4.1 Altersverteilung der Passagiere
Zunächst wurde die allgemeine Altersverteilung der Passagiere mithilfe der plot-Funktion für die Spalte "Age" ermittelt und als Histogramm (bins=20) ausgegeben.

### 4.4.2 Altersverteilung der Passagiere
Um eine genauere Betrachtung der absoluten Werte zu ermöglichen, wurden Bins mit einer festgelegten Größe von 10 Jahren definiert und mithilfe von pd.cut() eine neue Spalte "AgeBins" generiert. Die Überlebensrate und die Anzahl der Überlebenden wurde anschließend für die definierten Gruppen aggregiert und ausgdruckt. Ein gestapeltes Histogramm mit den erstellten Altersgruppen zeigt das Verhältnis von Verstorbenen zu Überlebenden an.

## 4.5 Überlebensrate von Passagieren mit Angehörigen
Im Rahmen der Betrachtung zur Überlebenswahrscheinlichkeit wurden ebenfalls der Ehestand, die Anzahl der Geschwister und/ oder Ehepartner und schließlich die Anzahl der mitgereisten Familienmitglieder miteinbezogen.

### 4.5.1 verheiratete und unverheiratete Frauen
Mithilfe der extrahierten Anreden aus der neuen Spalte "Address" wurden die Überlebensrate von verheirateten mit den unverheirateten Frauen abgeglichen.

### 4.5.2 Überlebensrate von Passagieren mit Geschwistern/Ehepartnern an Bord
Mithilfe der "SibSp"-Spalte wurden die Überlebensraten von Passagieren mit Geschwistern und/ oder Ehepartnern abgeglichen. Anschließend wird in einem Tortendiagramm illustriert, wie hoch die Überlebesrate anteilig ist für Passagiere mit keinem, ein, zwei, drei oder vier Geschwistern und/ oder Ehepartnern. Zusätzlich wird dies noch als Balkendiagramm dargestellt, um den Effekt von jedem weiteren zusätzlichen Geschwisterteil/ Ehepartner aufzuzeigen.

### 4.5.3 Überlebensrate von Passagieren mit Familienangehörigen an Bord
Zuletzt wird der Einfluss der Familiengröße auf die Überlebensrate mithilfe von groupby() aggregiert. Dabei zeigt der Mittelwert (mean) die Überlebensrate, die Anzahl (count) die Gesamtzahl der Passagiere mit der jeweiligen Anzahl an Angehörigen und die Summe (sum) die absolute Anzahl der Überlebenden der jeweiligen Gruppe. Hier zeigt sich, dass anscheinend Personen mit 3 mitreisenden Familienmitglieder die höchste Überlebenschance hatten im Vergleich zu Passagieren, die allein, zu zweit oder mit mehr als drei Angehörigen gereist sind. 

# 5. Korrelation und Überlebenswahrscheinlichkeit
## 5.1 Korrelationsmatrix
Um die wichtigsten Faktoren und ihren Einfluss auf die Überlebenswahrscheinlichkeit der Passagiere hervorzuheben, wurde mithilfe der Korrelationsfunktion corr() und mit dem Seaborn-Modul eine Korrelationsmatrix erstellt und eine Heatmap-Ansicht generiert. Die positiv-korrelierenden Faktoren sind rot bis braun, die negativ-korrelierenden Faktoren lila bis schwarz. Hier fällt auf, dass mit Abstand das Geschlecht, gefolgt von der Passagierklasse und dem Ticketpreis mit derÜberlebswahrscheinlichkeit korrelieren.
