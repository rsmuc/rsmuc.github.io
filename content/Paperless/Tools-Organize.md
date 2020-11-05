---
title: "Tools - 5 -: Dateien automatisch sortieren mit Organize"
sub: "Kann das nicht jemand anders tun? --> ja"
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/tools5-organize.png'
tags: ["papierloses Büro", "Automatisierung", "PDF", "Tools", "sortieren", "organize", "Linux", "Python"]
toc: true
---

Sein wir mal ehrlich. Das Thema papierloses Büro ist schon ein wenig lästig. Ist eben doch Papierkram. Ob dieser nun digital bei uns aufschlägt oder analog ... Das Ganze muss mindestens überflogen und sortiert werden.

Das einsortieren in die Ordnerstruktur ist zwar praktisch, wenn es um das Wiederfinden geht, aber einer der aufwändigsten Schritte. Allerdings können wir dies auch dies automatisieren. So müssen wir dann gar nichts mehr machen.

Mein erster Ansatz war: Anhand des Dateinamens verschiebe ich die Dokumente in den richtigen Ordner. Dies setzt voraus, dass die Dateinamen eindeutig sind, funktioniert aber erst mal ganz gut ...

	mv "*kontoauszug*.pdf" /home/ich/Dokumente/01_Bank/HVB/2020/Kontoauszüge/
	
	...

Nun gibt es aber immer wieder Dokumente, die nicht ganz so einfach zu identifizieren sind. Was, wenn wir nicht nur Kontoauszüge von der HVB haben, sondern auch noch von der comdirect Bank oder der Deutschen Bank und die Dateien dort sehr ähnlich heißen? Oder wir haben mehrere Konten bei einer einzelnen Bank? 

Dann hilft uns der Dateiname nicht mehr weiter.

Nun hätten wir noch die Dateiinhalte, anhand derer wir sortieren können. Die Idee ist einfach. Kommt das Schlagwort IBAN 12345678957445 und Kontoauszug im Dokument vor, dann wird es wohl ein Kontoauszug von unserem Konto mit der Nummer 12345678957445 sein. Aber mit einem Shell-Script kommen wir nicht einfach an die Inhalte des PDFs ran.

Ich hatte nun schon begonnen, mir wieder mittels Python ein Script zu schreiben, welches die Aufgabe übernimmt, da bin ich auf Organize gestoßen: <https://github.com/tfeldmann/organize>

## Organize

Organize kann mittels unterschiedlichster Kriterien Dateien sortieren. Dies kann der Dateinamen, der Inhalt, die Meta-Daten, die Größe und einiges mehr sein. Für uns ist vor allem der Dateiname und der Inhalt interessant. Anhand dieser Kriterien können dann Dateien weiterverarbeitet werden, also z. B. umbenannt, verschoben oder kopiert. Genau das was wir brauchen, um uns das Leben in Zukunft einfach zu machen.

### Installation

Die Installation ist schnell erledigt. Entweder es ist in den Repositorys oder AUR der Distribution enthalten oder man kann es mittels pip nachinstallieren:

	pip install organize-tool


---

***Randnotiz:***

Verwendet man Firejail auf seinem System, sollte man ggf. das Profil für pdftotext unter /etc/firejail/pdftotext.profile anpassen bzw. mittels einer pdftotext.local erweitern. pdftotext darf ansonsten nur im "Downloads"- und "Documents"-Ordner arbeiten.

---

Ob die Installation erfolgreich war, können wir so testen:

	organize --help	

### Konfiguration von Organize

Eine ausführliche Dokumentation ist hier zu finden: <https://organize.readthedocs.io>

Alle Aktionen, die Organize durchführen soll, werden über eine einzelne Konfigurationsdatei festgelegt.

Wo diese Datei liegt, können wir uns so anzeigen lassen:

	$ organize config --path
	/home/ich/.config/organize/config.yaml
	

Mittels `organize config` wird Konfigurationsdatei direkt im Standardeditor geöffnet.

Wie schon an der Dateiendung zu erkennen, handelt es sich um eine YAML-Datei, welche einen sehr einfachen Aufbau hat.

Es werden einfach die einzelnen Regeln nacheinander aufgelistet. Also z. B.:

	rules:
	
	  - folders: ~/Downloads
	    subfolders: false
	    filters:
	      - filename:
	          contains: 'PapierlosesBuero'
	    actions:
	      - move: "/home/ich/Dokumente/1 Blog/"
	      
	  - folders: ~/Downloads
	    subfolders: false
	    filters:
	      - filename:
	          contains: 'Linux'
	    actions:
	      - move: "/home/ich/Dokumente/2 Linux/"	      

Hat man alle Regeln definiert und die Datei gespeichert, einfach nur `organize run` ausführen und schon sollte organize die Regeln abarbeiten. Werden nun keine Dateien gefunden, welche ein Filter passt, sieht es so aus:

	$ organize run
	Nothing to do.

Trifft ein Filter zu, werden die definierten Aktionen ausgeführt:

	$organize run
	Folder /home/ich/Dokumente/Inbox/:
		File 2020-09-21 Rechnung Nutzerwechselgebühren [Steuer2020].pdf:
    			- [Copy] Copy to "/home/ich/Dokumente/4 Steuer/Einkommensteuer 2020/2020-09-21 Rechnung Nutzerwechselgebühren [Steuer2020].pdf.pdf"
    			- [Move] Move to "/home/ich/Dokumente/8 Wohnung/2020-09-21 Rechnung Nutzerwechselgebühren [Steuer2020].pdf [Steuer2020].pdf"


#### Kommentare einfügen

Damit man die Übersicht in der Konfiguration behält, kann man im YAML-File auch Kommentare einfügen. Alles, was mit einem `#` beginnt, wird ignoriert.

#### Arbeitsverzeichnisse definieren:

Möchte man nun, dass eine Regeln nicht für einen einzelnen Ordner gilt, sondern für mehrere, lässt sich folgendes Konstrukt anwenden:

	document_folders: &docs
	  - ~/Dokumente/Inbox
	  - ~/Downloads/Inbox
	
	rules:
	
	  - folders: *docs
	    subfolders: false
	    filters:
	      - filename:
	          contains: 'Linux'
	    actions:
	      - move: "/home/ich/Dokumente/2 Linux/"	 


Die Regel wird also auf alle definierten Verzeichnisse angewendet.

#### Filter kombinieren

Es lassen sich natürlich auch mehrere Filter miteinander kombinieren:

	  - folders: ~/Downloads/Inbox
	    subfolders: false
	    filters:
	      - filecontent: '123456789'
	      - filecontent: 'comdirect'
	      - filename:
	          contains: 'Kontoauszug'
	      - filename:
	          startswith: '2020-'
	    actions:
	      - move: "/home/ich/Dokumente/33 Bank/2020/Kontoauszüge/"	
	      


#### Actions

Organize hat diverse "Actions" zur Auswahl. Das vermutlich am häufigsten Verwendete: move

Man sollte bei der Move Action immer drauf achten, dass man das abschließende `/` nicht vergisst.

Richtig:

      - move: "/home/ich/Dokumente/2 Linux/"	

Falsch:

      - move: "/home/ich/Dokumente/2 Linux"	

Bei der ersten Variante wird die Datei korrekt in das gewünschte Verzeichnis verschoben.

Vergisst man das `/` am Ende, werden unsere Dateien als `/home/ich/Dokumente/2 Linux2`, `/home/ich/Dokumente/2 Linux3`, `/home/ich/Dokumente/2 Linux4` benannt. Das wäre unschön.


Es ist aber noch mehr möglich, so können Dateien mittels der "rename"-Action umbenannt werden:

      - rename: "{path.stem}.pdf"

Oder es können auch Aktionen auf der Shell ausgeführt werden. z. B.:

      - shell: 'docker run --rm -v {basedir}:/data -i jbarlow83/ocrmypdf "/data/{path.name}" "/data/{path.name}" -l deu --force-ocr'
      

Und auch Actions können mehrere miteinander in einer Regel kombiniert angewendet werden.

## Fazit

Hat man sich einmal seinen Regelsatz aufgebaut, hat man mit dem Sortieren der Dokumente keine Arbeit mehr. Der größte Teil der Dokumente ist immer wiederkehrend. Somit lohnt es sich, die Regeln einmalig anzulegen und ggf. immer mal wieder zu erweitern.

Für das papierlose private Büro ist Organize eine erhebliche Erleichterung.