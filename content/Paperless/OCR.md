---
title: "Schritt 2: Texterkennung (OCR) von PDFs unter Linux"
date: 2020-08-31T09:47:54+02:00
draft: false
featured_image: 'Paperless/titlepics/step2.jpg'
tags: ["OCR", "papierloses Büro", "Tesseract", "OCRmyPDF"]
toc: true
---

## Grundlagen

Im ersten Schritt haben wir uns darum gekümmert, dass wir unsere Dokumente eingescannt haben.
So weit, so gut. Die Dokumente liegen nun als PDF vor. Allerdings sind diese PDFs nicht durchsuchbar.
Wir können so zwar mehr Platz in unserem privaten Büro schaffen, aber viel mehr Komfort und Nutzen
sind noch nicht erreicht.

Hier kommt OCR ins Spiel. OCR steht für Optical Character Recognition, ins Deutsche meistens mit "Texterkennung"
übersetzt. Optische Zeichenerkennung wäre die korrektere Übersetzung. 

Am Ende soll in unserem PDF also nicht nur die Rastergrafik, die durch den Scanner erstellt wurde, sein, sondern
auch noch die Textebene mit der man das PDF durchsuchen kann. Dies bringt zwei Vorteile:

* Die Suche nach Dokumenten kann auch über deren Inhalt erfolgen (hierzu gibt es später einen eigenen Artikel).
Es muss also nicht immer nach Dateinamen gesucht werden.
* Inhalte können aus dem PDF herauskopiert werden. Besonders bei IBAN-Nummern u.ä. ist dies sehr praktisch. 
(Immer ein wenig aufpassen ... OCR ist nicht immer perfekt)

### Tesseract Geschichte

Die Software Tesseract ist die am häufigsten verwendete Software bzw. Library zur Texterkennung. Tesseract
steht unter der Apache License und ist somit Open Source. Viele kommerzielle Produkte setzen Tesseract unter
der Haube ein.

[Entwickelt](https://github.com/tesseract-ocr/docs/blob/master/das_tutorial2016/1Intro-history.pdf) 
wurde Tesseract ursprünglich ab 1985 von Hewlett-Packard als proprietäre Software.
1994 stellte HP die Entwicklung dann ein und Tesseract verschwand zunächst komplett von der Bildfläche.

2005 veröffentlichte HP den Source Code als Open Source und Google nahm sich dem Projekt 2006 an.
Seitdem wird Tesseract aktiv weiterentwickelt und wurde der De-Facto Standard, was das Thema OCR angeht.

Tesseract wird unter anderem auch bei Google Books und dem SPAM Filter von GMail eingesetzt.

### Funktionsweise von Tesseract und OCR

Während Texterkennung Anfangs nur für speziell entwickelte Schriftarten funktionierte und später
auf einzelne wenige Sprachen limitiert war, beherrscht Tesseract heute die Texterkennung in über 100
Sprachen und wurde mit über 4500 Schriftarten trainiert.

Eine einfache Zeichenerkennung führt bei normalen Dokumenten zu keinem zufriedenstellenden Ergebnis.
Ein l (kleines L) und ein I (großes i), sowie O (Buchstabe) und 0 (Zahl) sehen in vielen Schriftarten nahezu identisch
aus. Hier kann es also schnell zu Verwechslungen kommen. Tesseract arbeitete also nicht nur mit einer
einfachen Zeichenerkennung, sondern mittels ICR (Intelligent Character Recognition). Die einzelnen
erkannten Zeichen werden analysiert und gegen ein Wörterbuch und statistische Werte geprüft. Dies wird
so lange gemacht, bis ein vermeintlich valides Ergebnis entsteht. Es sind also nicht nur die
Schriftarten entscheidend, sondern auch die jeweilige im Dokument verwendete Sprache. Siehe auch
[Link](https://github.com/tesseract-ocr/docs/blob/master/das_tutorial2016/2ArchitectureAndDataStructures.pdf).

Mit Tesseract in der Version 4, welche im Jahr 2016 erschienen ist, gibt es einen großen Bruch in der Technik.
Durch die zunehmende Rechenleistung von PCs und Fortschritte im Bereich künstliche Intelligenz, verwendet
Tesseract nun ein neuronales Netz zur zeilenweisen Texterkennung von Dokumenten. Das neuronale Netz von 
Tesseract wurde mit Trainingsdaten in über 100 Sprachen, 4500 Schriftarten und je Sprache
circa 500.000 Zeilen trainiert. (Mehr Infos: 
[Link](https://github.com/tesseract-ocr/docs/blob/master/das_tutorial2016/7Building%20a%20Multi-Lingual%20OCR%20Engine.pdf)
). Hat man selbst eine sehr außergewöhnliche Schriftart in seinen
Dokumenten, könnte man Tesseract also selbst noch weiter trainieren, um bessere Ergebnisse zu erzielen.

Ein eigenes Training dürfte aber im Normalfall nicht notwendig oder sinnvoll sein. Erzielt Tesseract
schlechte Ergebnisse bei der Texterkennung, ist es meist sinnvoller zunächst die Eingangsdaten zu prüfen.
Stimmt die Qualität der Scans? Stimmt die Auflösung?

### OCRmyPDF

Die Grundlage für die OCR ist also Tesseract. Tesseract alleine reicht uns jedoch noch nicht.
Mittels der kleinen Python Software [OCRmyPDF](https://github.com/jbarlow83/OCRmyPDF) erhalten wir einige weitere Features:

* Verarbeitung von mehrseitigen PDFs als Input (Tesseract erwartet eine Bilddatei)
* Ausgabe als PDF/A (hierzu wird es noch einen eigenen Artikel geben)
* Automatisches drehen der PDF Seiten
* Optimierung der Eingabedatei (Entfernung von Verzerrungen, gerade richten von Seiten, entfernen von 
Scan-Artefakten)
* Setzen eines Titels im PDF 

OCRmyPDF hat eine sehr ausführliche Anleitung, die unter <https://ocrmypdf.readthedocs.io/en/latest/>
zu finden ist.

## Anwendung

Dies hört sich nun alles schon sehr kompliziert an. In der Praxis kommen wir aber nur mit OCRmyPDF in
Berührung und alles weitere erfolgt im Unterbau. Es wird also nur ein einzelnes Kommando
benötigt.

Auch für Linux gibt es mehrere Scan-Tools, welche Tesseract direkt über die GUI nach dem Scan ansteuern.
Ich bin jedoch der Meinung, dass man hier über die Kommandozeile effizienter unterwegs ist. Alle gewünschten
Parameter sind eindeutig definiert und man muss nicht bei jedem Scan darauf achten, ob sich eventuell ein
Schalter in der GUI verstellt hat.

Von OCRmyPDF gibt es einen offiziellen (Docker) Container, welchen ich verwende. Ursprünglich habe ich die
"normale" Installation verwendet. Eines Tages hat mir hier jedoch meine rolling-release Distribution 
Manjaro in die Suppe gespuckt und  einige Abhängigkeiten gingen kaputt. Bis dies durch 
Manjaro behoben war, dauerte es 2 Wochen und so sah
ich mich nach einer Alternative um. Der Container bringt den Vorteil mit sich, dass alle Abhängigkeiten,
also auch z.B. Tesseract, durch den Entwickler von OCRmyPDF getestet werden und somit kann man sicher sein,
einen gut funktionierenden konsistenten Zustand zu haben.

[Docker](https://www.docker.com/) oder [Podman](https://podman.io/), die zum Ausführen des Containers 
verwendet werden, sind unter den meisten 
Distributionen mittlerweile sehr schnell installiert. Bei Manjaro ist beides in den offiziellen
Repositories enthalten. Ich selbst verwende derzeit Docker zur Ausführung.

Eine ausführliche Anleitung zur Verwendung des Containers ist hier zu finden: 
<https://ocrmypdf.readthedocs.io/en/latest/docker.html>

Um sich das Container Image aus dem Docker Hub zu ziehen:

    docker pull jbarlow83/ocrmypdf
    
Anschließend sollte folgendes zur Ausgabe der Versionsnummer führen:

    docker run --rm -i jbarlow83/ocrmypdf --version
    10.3.0.post3+g0287d91.d20200727
    
Und schon können wir OCRmyPDF verwenden:

    find -name "*.pdf" | xargs -i docker run --rm -v $(pwd):/data jbarlow83/ocrmypdf /data/{} /data/{} -l deu --rotate-pages --title {} --clean --rotate-pages-threshold 5


Ups ... der Aufruf sieht doch ein wenig kompliziert aus. Damit es später in der Bedienung einfacher wird,
kann man dies einfach in ein kleines Shell-Script packen. Aber was passiert dort nun eigentlich:

* `find -name "*.pdf" | xargs` : Es werden alle Dateien im Verzeichnis mit der Endung *.pdf gesucht
und die Ergebnisse an xargs zur weiteren Verarbeitung übergeben. Werden mehrere PDF-Dateien gefunden,
wird der nachfolgende Befehl (also ocrmypdf) für jede PDF-Datei einzeln aufgerufen und jeweils der
Dateiname übergeben.

* `docker run --rm -v $(pwd):/data`: Das aktuelle Arbeitsverzeichnis wird innerhalb des Containers
verfügbar gemacht. OCRmyPDF, das ja im Container arbeitet, kann nun also auf alle Dateien des 
aktuellen Arbeitsverzeichnisses zugreifen.

* `jbarlow83/ocrmypdf /data/{} /data/{}`: Das Ausführen von OCRmyPDF - wir übergeben den Dateinamen
des PDFs als Input- und als Ausgabename. Wir überschreiben also das ursprüngliche PDF. OCRmyPDF
überschreibt die Datei nur, wenn es zu keinen Fehlern gekommen ist. Möchte man dies nicht, kann man
natürlich auch einen anderen Dateinamen als Ausgabenamen übergeben. z.B. `/data/ocr-{}`. Da jedoch
die Datei ohne Textebene nicht mehr benötigt wird, überschreibe ich diese gleich.

* `-l deu`: Es wird an Tesseract übergeben, dass Deutsch als Sprache zu erwarten ist.
Dies ist eine sehr wichtige Option, um die Qualität der Texterkennung zu steigern. 

* `--rotate-pages`: OCRmyPDF soll Seiten in die korrekte Richtung drehen. Also z.B. um 90°.

* `--title {}`: Der Dateiname soll als Titel im PDF gesetzt werden

* `--clean`: Vor der Texterkennung mittels Tesseract, sollen mittels Unpaper vorhandene Scan-Artefakte,
also z.B. Staubkörner etc. entfernt werden, um die Texterkennung zu verbessern. Diese optimierte
Grafik wird jedoch nur für die Erkennung verwendet und nicht ins PDF übernommen. (Dies würde --clean-final machen.)
Hier besteht jedoch die Gefahr, dass Inhalte gelöscht oder verändert werden. Ich habe lange Zeit --clean-final
ohne negative Auswirkungen verwendet. Mittlerweile habe ich jedoch davon abstand genommen. Am Original
soll so wenig wie notwendig verändert werden.

* `--rotate-pages-threshold 5`: Hier wird der Threshold für das Rotieren der Seiten etwas herab gesetzt.
`5` hat sich bei mir als guter Wert etabliert.

Optional biete sich noch die Option `--deskew` an. Ist der Scan leicht schief, weil das Papier
schief eingezogen wurde, kann dieser mittels der --deskew Option gerade gerückt werden. Das Ergebnis
wird ins abschließende PDF übernommen. Dies kann zu schöneren PDFs und auch zu einer besseren Texterkennung
führen. Ich persönlich nutze diese Option jedoch nicht, da dies bei mir deutlich größere Dateigrößen
zur Folge hat. Zudem funktioniert der automatische Einzug beim Brother Scanner sehr zuverlässig und
es kommt nur selten zu einer Schiefstellung.

Als Beispiel ein 54-seitiges PDF:

* Ohne OCR: 5,8 MB
* Mit OCR: 7,7 MB
* Mit OCR und deskew: 13 MB

Führt man das genannte Kommando nun aus, hat man nach kurzer Zeit also nur noch PDFs inkl. Text-Layer
im Arbeitsverzeichnis. (Ein Backup aller Dateien im Arbeitsverzeichnis, kann vor dem ersten Ausführen
nicht schaden.)

Das Ergebnis kontrolliert man am einfachsten, wenn man nun das PDF mit einem PDF-Viewer öffnet, alles markiert
und in einen Texteditor kopiert. Nun kann man den erkannten Text mit dem Original vergleichen.
Alternativ kann man auch die --sidecar Option von OCRmyPDF verwenden. Dann wird der erkannte Text,
zusätzlich nicht nur ins PDF geschrieben, sondern auch in eine Textdatei. Mir hat bis jetzt die Variante
mit dem PDF-Viewer immer ausgereicht.

Nun haben wir also sauber gescannte PDFs mit Textebene, Titel und korrekt rotierten Seiten.