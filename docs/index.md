# Konzeption und prototypische Entwicklung eines oXygen-basierten Frameworks zur Edition osmanischer Liedtexte. Unterstützt durch ein Leitfadeninterview zur Erhebung des Vorwissens der perspektivischen Nutzerinnen- und Nutzergruppe.

### Zielsetzung
Im Rahmen der gleichnamigen Masterarbeit wurden zuerst die Grundlagen der (digitalen) Edition dargestellt. Der Schwerpunkt lag dabei auf der Nachzeichnung des Editionsprozesses bis hin zu Editionswerkzeugen.
Anhand der Theorie wurde ein Leitfadeninterview entwickelt, das mit Wissenschaftlerinnen und Wissenschaftlern, die an einer kritischen Edition osmanischer Liedtexte beteiligt sind, geführt wurde. Das Leitfadeninterview wurde qualitativ ausgewertet. Grundlage bildeten die folgenden deduktiv festgelegten Kategorien:

1. individuelle Vorkenntnisse
1. individuelle Erfahrungen
1. Arbeitsweisen und technische Terminologie
1. Nutzerinnen- sowie Nutzerkreis und Nachnutzung

Zusätzlich wurde quantitativ analysiert, ob ein Zusammenhang zwischen Vorkenntnissen und dem Einsatz von Verzögerungsmarkern in den einzelnen Antworten nachzuweisen ist.

Auf dieser Grundlage wurden Gespräche mit den Wissenschaftlerinnen und Wissenschaftlern geführt, um die Vorkenntnisse und Erfahrungen zu erweitern und anschließend Anforderungen für das Framework zu erfassen.

Anforderungen:

1. Die Auszeichnung der osmanischen Liedtexte soll die bisherigen Möglichkeiten einschließen, das heißt, folgende Merkmale sollen zusätzlich zu den Metadaten ausgezeichnet werden können:
    1. Überschriften
    1. einzelne Verse mit den Analysemöglichkeiten Terennün und Hauptvers des Liedtextes
    1. Aufführungsanweisungen
    1. Lemmata und Lesarten 
    1. Provenienz
    1. editorische Anmerkungen
    1. Versmaß innerhalb der Metadaten

1. Reduktion der Komplexität der Benutzeroberfläche
1. Einbinden von Schaltflächen für die häufigsten Auszeichnungsschritte
1. Die Auszeichnung soll den TEI-Standards entsprechen.

### Umsetzung

Das künftige Editionswerkzeug soll oXygen Author sein, da hier bereits die  Benutzeroberfläche vereinfacht ist.
Das Framework wurde extern angelegt, um es später den Editorinnen und Editoren bereitstellen zu können. Zusätzlich wurde eine Verknüpfungsregel eingeführt, die besagt, dass das Framework nur bei XML-Dokumenten greift, die auf *_cmo.xml, *.cmo.xml, *_CMO.xml oder *.CMO.xml enden:

![Verknüpfungsregel](/Framework/verknuepfungsregel.png)

Danach wurde das Schema eingebunden, das mithilfe des Dienstes [Roma - ODD Customization](https://romabeta.tei-c.org/) reduziert wurde:

![Schemaeinbindung](/Framework/schemaeinbindung.png)

Für die Anpassung der Oberfläche wurde ein CSS eingebunden, das auf vorhandene CSS-Dokumente zugreift, die im oXygen-TEI-Framework enthalten sind:


![CSS-Einbindung](/Framework/csseinbindung.png)

Das CSS wurde insofern angepasst, dass der Bereich der Metadaten in Teilen oder vollständig einklappbar ist, um eine möglichst fokussierte Arbeit am zu edierenden Text zu ermöglichen:

![Einklappbarer Metadatenteil](/Framework/faltbar.png)

Darüber hinaus wurde die Symbolleiste erweitert. Dazu mussten Aktionen innerhalb des Frameworks definiert werden:

![Übersicht Aktionen](/Framework/aktionen.png)

Alle diese Aktionen mussten mit einer einzigartigen ID, einem Namen und einer Beschreibung angelegt werden.

Danach wurden ein Icon zugeordent, der Geltungsbereich, in dem die Aktion ausgeführt werden kann mittels eines XPath-Ausdrucks festgelegt und ein Vorgang ausgewählt. Für alle Aktionen wurde ausgewählt, dass Text, der angewählt wird, wenn die Schaltfläche betätigt wird, von einem Element umschlossen wird oder dies rückgängig gemacht wird, falls das entsprechende Element schon den Text umschließt:

![Anpassung der Aktionseinstellungen](/Framework/akteinstellung.png)

Das Element, mit dem der Text eingeschlossen wird, wird als Argumentwert übergeben. Wichtig ist hierbei, dass der namespace der TEI angegeben wird, damit das Element vom Schema erkannt wird. Gleichzeitig können Attributwerte sofort mit angelegt werden wie im konkreten Beispiel zu sehen ist:

![Argumentwert festlegen](/Framework/argument.png)

Die definierten Aktionen können dann in der Symbolleiste eingebunden werden:

![Einbindung von Aktionen in die Symbolleiste](/Framework/symmenue.png)

Die Festlegung des Geltungsbereiches bietet den Vorteil, dass die Aktionen nur dann zur Verfügung stehen, wenn sich im entsprechenden Bereich des edierten Textes befunden wird. Da in den Metadaten beispielsweise laut Schema keine Verse ausgezeichnet werden dürfen, wurde dies so im XPath-Ausdruck bestimmt und die Schaltfläche ist ausgegraut, wenn sich im Metadatenteil befunden wird:

![Verfügbarkeit der Schaltflächen im teiHeader-Element](/Framework/symboleng.png)

Soll eine Aktion hingegen aus dem zu edierenden Stück heraus erfolgen, stehen wesentlich mehr Aktionen zur Verfügung:

![Verfügbarkeit der Schaltfläche im text-Element](/Framework/symbolweit.png)

Der Prototyp des Frameworks ist weiter beliebig anpassbar. Es wurde mit einem projektspezifischen Template den Mitarbeiterinnen und Mitarbeitern des Projektes zur Verfügung gestellt, die die osmanischen Liedtexte edieren und steht gleichzeitig im [GitRepositorium](https://github.com/maxweberstiftung/CMO-prototype-framework-text-edition) der Max Weber Stiftung öffentlich zur Verfügung, da diese für den Bereich Digital Humanities im Projekt zuständig ist.
