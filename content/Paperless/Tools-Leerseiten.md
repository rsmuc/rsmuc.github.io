---
title: "Tools - 3 -: Leerseiten entfernen"
sub: "Weg mit unnötigem Ballast"
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/tool3-leerseiten.png'
tags: ["papierloses Büro", "Leerseiten", "PDF", "Tools", "empty", "blank", "Linux", "Python"]
toc: true
---

Unser Dokumentenscanner erfasst immer die Vor- und die Rückseite eines Blattes in einem Durchgang. Nun gibt es aber natürlich immer wieder Dokumente, die nur einseitig bedruckt sind. Das Ergebnis: Eine weiße Seite im PDF. 

Je nach Scanner und verwendeter Software lässt sich einstellen, dass diese Seiten gleich übersprungen werden. Bei meiner Kombination, dem Brother ADS-1200 und Simple Scan, ist dies nicht möglich. 

Nun könnten wir in Simple Scan händisch jede leere Seite löschen,  bevor wir das Dokument als PDF abspeichert. Oder wir ignorieren einfach, dass dort leere Seiten erfasst wurden und speichern diese mit. Leere Seiten belegen nur sehr wenig Speicherplatz. Das einzig unschöne: Beim Lesen von Dokumenten stören diese ein wenig.

Dass eine leere Seite wenig Speicherplatz benötigt, können wir uns mittels eines kleinen Python-Scripts zunutze machen und somit leere PDF-Seiten finden und entfernen:

<https://github.com/rsmuc/paperless/blob/master/blank3.py>

Zunächst müssen die Abhängigkeiten installiert werden:

	pip install PyMuPDF
	pip install PyPDF2

Führen wir nun mittels `python blank3.py` das Script aus, werden alle PDFs im Verzeichnis nach leeren Seiten durchsucht. Werden leere Seiten gefunden, wird:

* Eine Kopie der Originaldatei angefertigt mit der Endung: _ORIGINAL_
* Eine Datei mit allen leeren Seiten angelegt mit der Endung: _EMPTYPAGES_
* Ein neues Dokument mit dem ursprünglichen Namen, welches keine Leerseiten mehr enthält

Nach dem Ausführen sollte man immer prüfen, ob auch wirklich nur komplett leere Seiten entfernt wurden.

Im Script wird die Größe jeder Seite geprüft. Ist diese kleiner als der im Script eingestellte Threshold (7000 Bytes), wird die Seite als leer erkannt.

Somit können wir nun also nach dem Scannen bequem alle leere Seiten entfernen und haben ein wenig mehr Ordnung in unseren Dateien.

	$ python blank3.py 
	./2020-08-17 Testdatei.pdf
	Size page 1: 122145
	Size page 2: 119844
	Size page 3: 6298
	below threshold
	...	
	create a copy of the ./2020-08-17 Testdatei.pdf
	Empty pages: [3, 5, 9, 13, 15, 17]
	Generate file with empty pages
	Generate clean file

Das Entfernen der Leerseiten sollte man immer vor OCRmyPDF durchführen. Macht man dies bei einem PDF/A-File, wird dieses im Anschluss von veraPDF als nicht-valide eingestuft.

---
***Randnotiz:***

Man könnte mittels Ghostscript auch die Farbabdeckung auf de rSeite ermitteln und anhand dieser die leeren Seiten erkennen. Oder man könnte erst das OCR durchführen und prüfen, ob ein Text erkannt wurde. (Wenn eine Seite allerdings nur ein Bild enthält, hat man ein Problem)

---  