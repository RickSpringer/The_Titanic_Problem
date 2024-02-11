# The_Titanic_Problem

## 1. Einleitung

### 1.1 Datengrundlage & Fragestellung
Das Projekt, 'The Titanic Problem', ermittelt mithilfe verschiedener Datenanlyse-Methoden Indikatoren, die einen Einfluss auf das Überleben der einzelnen Passagiere hatten. Die Faktoren werden in einem zusammengefassten Jupyter Notebook ("The Titanic Problem Notebook") ermittelt und ihr Einfluss mit einfachen Plots illustriert. Als Datensatz wurde der Datensatz "titanic.csv" bereitgestellt. Unter "2. Datenerfassung" wird genauer auf die bereitgestellten Daten, das Format, Typ und Ähnliches eingegangen.

### 1.2 Module, Methoden & Bedingungen
Zur Ausführung des Projekt-Notebooks werden folgende Module in Python benötigt:
- Jupyter 1.0
- Matplotlib 3.8.2
- Pandas 2.2.0

## 2. Datenerfassung
### 2.1 Beobachtungen & Fragen
Der Datensatz umfasst *12 Spalten* und 891 Zeilen mit Informationen zu Passagieren der Titanic. Anbei eine Übersicht der Spalten und der hinterlegten Informationen:
**1. 'PassengerId'**
Enthält die PassagierId als Integer. Die hinterlegten Zahlen stehen für die IDs und reichen von 1 - 891.

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

*d.  Enthält verschiedene Titel und Anreden. Titel [], Anreden []*

*e.  '.' = konstanter Separator nach 'Address'*

*f.  {Vornamen} = ein oder mehrere Vornamen. Wird in neue Spalte **'First Name'** ausgegliedert. Die einzelnen Vornamen sind durch ' ' getrennt. Wenn 'Address' nicht 'Miss' ist, werden zuerst die Vornamen des Ehemanns angegeben.*

*g.  {Mädchenname} = Mädchenname. Wird in neue Spalte **'Maiden Name'** ausgegliedert. Wenn Titel/Anrede 'Mrs' ist, wird am Ende der Mädchenname in Klammern angegeben, z.B. (Florence Briggs Thayer). Spitznamen sind teilweise in Anführungszeichen angegeben, z.B. "Frankie"*
                                                                        
**5. 'Sex'**
Enthält das Geschlecht des Passagiers als String. Entweder 'female' für weiblich oder 'male' für männlich.

**6. 'Age'**
Enthält das Alter des Passagiers in Jahren als Float. Die Altersangaben, bsp. von Kindern unter einem Jahr, deuten darauf, dass bei der Datengenerierungen Berechnungen abgelaufen sind, die Floats mit bis zu zwei Nachkommastellen produziert habem. Wie diese Berechnung ablief, ist nicht zu rekonstruieren.

**7. 'SibSp'**
Enthält die Geschwisteranzahl des Passagiers als Integer.

**8. 'Parch'**
Enthält Informationen zum Zustand der Umgebung?!

**9. 'Ticket'**
Enthält Ticketnamen als String. Diese Bezeichnungen setzten sich entweder nur aus Zahlen, aus einer Buchstabenfolge und Zahlen oder einer Kombination aus Sonderzeichen, Buchstaben und Zahlen.

**10. 'Fare'**
Enthält den Ticketpreis als Float mit 4 Nachkommastellen. Die Währung ist nicht angegeben.

**11. 'Cabin'**
Enthält den Namen der Kabine des Passagiers als String. Setzt sich zusammen aus Buchstaben und Zahlenfolge, bsp. 'C85', 'E46'.

**12 'Embarked'**
Enthält den Ort, an dem der Passagier zugestiegen ist als String. S = Southampton (England), C = Cherbourg (Frankreich), Q = Queenstown (Irland).
