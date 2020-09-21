---
title: "Tools - 4 -: Dateiname automatisch mit Datum versehen"
sub: ""
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/tools4-date.png'
tags: ["papierloses Büro", "Datum", "PDF", "Tools"]
toc: true
---

Gerade bei Dokumenten, die wir aus den Online-Postfächern von Banken und Versicherungen herunterladen, kann die Weiterverarbeitung manchmal lästig sein. Jedes Dokument händisch umbenennen, damit das Datum im ISO-Format vorangestellt wird?

Das lässt sich auch zu einem gewissen Grad automatisieren. Gehen wir davon aus, dass das erste Datum, welches in einem Dokument vorkommt, das Ausstellungsdatum ist. Also können wir einfach die komplette Textebene nach dem ersten Datum durchsuchen und dann die Datei automatisch benennen.

Um sicherzustellen, dass wir eine Datei nicht komplett unsinnig benennen, machen wir dies nur wenn das aktuelle Datum vom gefundenen Datum nicht mehr als -20 oder +1 Tag abweicht. Post aus der Zukunft? Dann würde etwas nicht passen? Ein Dokument das angeblich älter als 20 Tage ist, aber wir jetzt erst heruntergeladen haben? Auch das ist verdächtig. Da schauen wir dann lieber selbst nach.

Genau diese Aufgabe übernimmt das hier verlinkte Python Script: <https://github.com/rsmuc/paperless/blob/master/setdate.py>

	$ python setdate.py 
	------------------------------------------------------
	./2020-08-17 Brief.pdf already has a date
	------------------------------------------------------
	Guessing the date for file in content./Test1.pdf
	FOUND DATE: 2020-09-03
	Difference to today: 13 days, 23:20:51.742015
	Rename to '2020-09-03 Test1.pdf'
	------------------------------------------------------
	Done


Vor der Ausführung muss die Abhängigkeit installiert werden:

	pip install pdfminer


Dies kann uns schon einiges an Arbeit abnehmen...