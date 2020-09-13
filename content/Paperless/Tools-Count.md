---
title: "Tools - 1 -: PDF Seiten zählen"
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/pages.png'
tags: ["papierloses Büro", "zählen", "Tools", "PDF"]
toc: true
---

## PDF-Seiten zählen

Das ganze Büro ist nun also digitalisiert und papierlos. Aus reiner Neugier wollte ich nun wissen: Wie viele Seiten PDFs habe ich jetzt eigentlich.

Dateien zu zählen ist einfach:

	$ find . -type f -iname '*.pdf' | wc -l
	3214

Wir suchen also nach allen Dateien mit Dateiendung PDF und zählen diese. 3214 Dateien. Das ist ja schon mal interessant.

Aber ich habe PDFs, die nur eine Seite umfassen und auch PDFs, die 50 Seiten und mehr umfassen. Also möchte ich auch noch die Seiten zählen. Dies ist nicht mehr ganz so einfach. OK, auch nicht sonderlich schwer.

Ich habe dazu ein kleines Python Script geschrieben. Sorry, der Code ist nicht sehr schön ... Aber es funktioniert :). Das Script setzt eine Installation von "pdfinfo" voraus.

Herunterladen könnt ihr das Script "count.py" hier: [Github Link](https://github.com/rsmuc/paperless/blob/master/count.py)

Einfach in das Dokumentenverzeichnis kopieren und ausführen:

	python count.py
	...
	...
	./11 Sonstiges/2018/DokumentXY.pdf: 5 pages; in total: 16357
	...
	...
	ALL PAGES: 16465

Also knapp 16500 Seiten. In einen normalen Aktenordner passen circa 500 Seiten. Dies entspricht also 33 Aktenordnern. In ein Kallax-Regal von Ikea mit 8 Fächern (150 x 75 cm) würden insgesamt 32 Ordner passen. Ich denke, das Digitalisieren hat sich also gelohnt.

---

***Randnotiz:***
Ich habe hier auch die Dateien mitgezählt, die ich bereits als PDF bekommen habe.

---