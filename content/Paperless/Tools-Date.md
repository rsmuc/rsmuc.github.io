---
title: "Tools - 4 -: Dateiname automatisch mit Datum versehen"
sub: ""
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/tools4-date.png'
tags: ["papierloses Büro", "Datum", "PDF", "Tools", "Automatisierung"]
toc: true
---

Gerade bei Dokumenten, die wir aus den Online-Postfächern von Banken und Versicherungen herunterladen, kann die Weiterverarbeitung manchmal lästig sein. Jedes Dokument händisch umbenennen, damit das Datum im ISO-Format vorangestellt wird?

Das lässt sich auch zu einem gewissen Grad automatisieren. Das Erstellungsdatum, also das Datum, wann es gespeichert wurde, zu verwenden wäre einfach. Allerdings ist dies auch wenig sinnvoll. Denn das Datum des Downloads oder das Datum des Scans kann vom eigentlichen Datum des Dokuments deutlich abweichen. Interessant ist ja das aufgedruckte Datum. Aber auch an dieses kommen wir dank OCR ran.

Gehen wir davon aus, dass das erste Datum, welches in einem Dokument vorkommt, das gewünschte Datum ist. Also können wir einfach die komplette Textebene nach dem ersten Datum durchsuchen und dann die Datei automatisch benennen.

Um sicherzustellen, dass wir eine Datei nicht komplett unsinnig benennen, machen wir dies nur, wenn das aktuelle Datum vom gefundenen Datum nicht mehr als -30 oder +1 Tag abweicht. Post aus der Zukunft? Dann würde wohl etwas nicht passen. Ein Dokument, das angeblich älter als 30 Tage ist, aber wir jetzt erst heruntergeladen haben? Auch das ist verdächtig. Da schauen wir dann lieber selbst nach.

Genau diese Aufgabe übernimmt das hier verlinkte Python Script: <https://github.com/rsmuc/paperless/blob/master/setdate.py>

	$ python setdate.py 
	------------------------------------------------------
	Guessing the date for file in content./ocr_beispiel.pdf
	FOUND DATE: 2020-09-13
	Difference to today: 11 days, 9:33:15.593419
	OK
	Rename to '2020-09-13 ocr_beispiel.pdf'
	------------------------------------------------------
	Done


Vor der Ausführung müssen nur die Abhängigkeiten installiert werden:

	pip install pdfminer
	pip install python-dateutil


Anschließend einfach ausführen und alle PDFs im aktuellen Verzeichnis werden mit dem richtigen Datum versehen. Dies kann uns schon Einiges an Arbeit abnehmen ...