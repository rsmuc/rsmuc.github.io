---
title: "Schritt 5: Das Backup und Versionierung"
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/step5.png'
tags: ["papierloses Büro", "Backup", "Versionierung", "Git", "Backintime"]
toc: true
---

In Schritt 4 haben wir uns nun also Gedanken gemacht, wie wir unsere Dokumente strukturiert ablegen. Es fehlt also kaum noch etwas, um mit der Arbeit wirklich loszulegen.

Zwei wichtige Punkte sollten nicht unter den Tisch fallen: Backup und Versionierung.

Wir digitalisieren alle unsere Papierdokumente mit dem Ziel, dass wir die Originale vernichten können und somit Platz und Ordnung im Büro haben. Ein passendes Dateiformat und eine passende Struktur sind ein guter Startpunkt. Aber wo liegen die Daten physikalisch? Erst einmal nur auf dem eigenen Notebook oder PC. Dies ist auch gut so. Aber was passiert, wenn wir eine Datei versehentlich löschen? Wenn wir eine Datei versehentlich verändern? Ein Virus (ok ... mit Linux eher unwahrscheinlich) unsere Daten verschlüsselt? Die SSD kaputt geht oder gar das ganze Büro inkl. unserem Rechner abbrennt?

## Backup

Für all diese Fälle brauchen wir ein Backup. Mit einem Backup wollen wir sicherstellen, dass wir jederzeit zu einem definierten Stand unserer Dokumente zurückkehren können. Es gibt ganze Bücher über Backup-Konzepte und je nach Anforderung können diese ganz unterschiedlich aussehen.

Das Backup für mein privates papierloses Büro hat zwei Ebenen. Das automatische Backup und das Offline-Backup.

### Das automatische Backup

Mit dem automatischen Backup möchte ich mich vor allem gegen ein versehentliches Löschen von Dateien absichern. Schnell hat man irgendeinen Blödsinn gemacht und plötzlich einen Ordner gelöscht.

Wie kommen wir nun also wieder zu unserem eingescannten Dokument zurück?

Backup-Tools gibt es viele. Aus meinen Mac-Zeiten kannte ich die Apple Timemachine, welche alle paar Minuten ein Backup des Macbooks angefertigt hat. Alte Backups wurden automatisch nach einiger Zeit aufgeräumt.

Unter Linux wurde ich mit "Back In Time" fündig. Das Prinzip ist das gleiche. Es werden alle paar Minuten Snapshots angelegt und man kann Schritt für Schritt in die Vergangenheit zurückgehen. Hat man dann seine Datei wieder gefunden, kann man auch nur diese einzelne Datei selektieren und wieder herstellen oder auch vollständige Verzeichnisse. Also alles sehr komfortabel und übersichtlich.

"Back In Time" ist in so ziemlich allen Distributionen enthalten, kann also einfach über den jeweiligen Paketmanager installiert werden.

 ![BackInTime](2482) 
 
 Nach dem Start sollte man in den "Settings" festlegen, wie oft ein Snapshot erstellt werden soll. Alle 30 Minuten ist ein Wert mit dem ich nun seit mehreren Jahren gut zurechtkomme. 
 
 Unter "Include" wird nun noch ausgewählt, welches Verzeichnis bzw. welche Verzeichnisse gesichert werden sollen. Ich habe bei mir das komplett Home-Verzeichnis gewählt. Bei "Exclude" habe ich vor allem das Verzeichnis mit meinen virtuellen Maschinen angegeben. Hier macht ein Backup keinen Sinn.
 
 Meine Settings für "Autoremove", also das entfernen von alten Backups könnt ihr auf dem folgenden Screenshot sehen:
 
![BackinTime Autoremove](2483) 
  
In den "Expert Options" sollte eingestellt sein, dass Back In Time als Cron-Job läuft. Dies ist aber sowieso der Standard. 

Nun sollte sich alle 30 Minuten Back In Time kurz zu Wort melden und in der Notification-Bar anzeigen, dass es gerade ein Backup ausführt.

Das erste Backup kann natürlich ein wenig länger dauern. Von da an sollte alles ziemlich flott gehen.

Neben dem lokalen Modus, wie von mir verwendet, könnte man Back In Time auch so einstellen, dass es auf ein NAS oder Ähnliches sichert. Da ich jedoch kein NAS habe (und auch keines will), reicht mir der lokale Modus aus.

Nun sollte man unbedingt ein Backup-Konzept testen. Das beste Konzept und Tool hilft nicht, wenn es nicht funktioniert oder man es nicht bedienen kann. Also im Home-Verzeichnis eine Test-PDF ablegen, warten bis ein Snapshot erstellt wurde, das PDF löschen und schauen, ob die Wiederherstellung klappt.
  

### Das Offline- / Offsite-Backup

Das lokale Backup von "Back in Time" beschützt mich zwar vor einem ungewollten Löschen von Dateien, aber vor einem Festplatten-Schaden oder gar Schlimmeren nicht. Denn die Daten liegen alle trotzdem nur auf meinem Notebook mit einer einzigen SSD.

Hier muss also noch eine andere Lösung her. Zunächst müssen wir also kurz die Anforderungen abstecken:

Das Offline-Backup sollte folgende Eigenschaften haben:

* Unabhängig von Betriebssystem, spezieller Hardware oder einer speziellen Applikation
* Kostengünstig
* Keine Cloud-Lösung
* Sicher
* Auch von Dritten lesbar. Dieser Punkt braucht ein wenig mehr Erläuterung: Ich will natürlich nicht, dass irgendjemand auf meine Dokumente zugreifen kann. Mein Notebook ist deshalb auch mit einer Festplattenverschlüsselung geschützt. Allerdings muss es möglich sein, dass im Falle meines Todes oder wenn ich anderweitig nicht mehr in der Lage bin, mich um meine Angelegenheiten zu kümmern, jemand Zugriff auf meiner Unterlagen erlangt.
* Maximaler Verlust von Daten der letzten 30 Tage
* Unveränderbar

Es gibt hier viele Möglichkeiten. Auch hier habe ich mich wieder für das Einfachste entschieden. Obwohl ich mittlerweile alle meine Dokumente digitalisiert habe, ist mein Dokumentenordner nur ~ 3 GB groß. Dies passt also wunderbar auf eine DVD.

Ich brenne also einfach am Ende eines jeden Monats eine DVD mit allen meinen Dokumenten. Diese DVDs werden gesammelt und bei Gelegenheit in einem Bankschließfach deponiert. Somit sind auch im Falle eines Brandes nicht alle Dokumente verloren. Ich mag zwar nur alle 6 Monate die DVDs ins Schließfach stecken, aber die Dokumente von 6 Monaten zu verlieren ist in einem solchen Fall verschmerzbar ... Nach einem Brand gibt es Schlimmeres. 

Die gebrannten DVDs sind zudem unveränderbar. Ein Virus und Ähnliches kann einen USB-Stick oder eine Festplatte als Backupmedium im Zweifelsfall beschädigen. Bei einer DVD kann dies nicht passieren.

Zudem habe ich schon zu viele defekte Festplatten und USB-Sticks gesehen. Defekte DVDs? Ja auch das kommt vor. Aber wenn eine Sicherung mal ausfallen sollte, habe ich ja für jedes Monat ein vollständiges Backup.

Wer ganz auf Nummer sicher gehen möchte, kann auch [M-Discs](https://www.verbatim.de/de/cat/mdisc-archival-media/) verwenden. Diese sind ein wenig teuer als normale DVD- oder Blueray-Rohlinge, sollen aber angeblich bis zu 1000 Jahre halten und sind unempfindlich gegen Sonneneinstrahlung und andere Umwelteinflüsse. Es gibt auch noch mehrere andere Standards für Rohlinge, welche eine sehr lange Lebensdauer garantieren sollen. Mir reichen normale DVD-Rohlinge. Was durchaus Sinn macht: Zwei unterschiedliche Hersteller oder Chargen verwenden. Dass die Rohlinge einer einzelnen Spindel aufgrund von chemischen Alterungsprozessen gleichzeitig nicht mehr lesbar werden, ist somit ausgeschlossen.

Viele Notebooks und auch Workstations kommen heute jedoch ohne optisches Laufwerk, da die meisten Anwendungen über App-Stores oder Downloads vertrieben werden. DVD- und Blueray-Brenner mit USB-Anschluss gibt es jedoch in einer großen Auswahl für wenig Geld. Ich würde gleich zu einem Blueray-Brenner raten, dann kann man auch seine Bildersammlungen etc. sichern und dieser kostet nur ein paar wenige Euro mehr. Ich selbst nutze einen Verbatim Slimline Blue-Ray Brenner (ca. 85 €).

Zum Brennen der DVDs verwende ich "Brasero".

 ![Brasero](2547) 

Meine Backups werden unverschlüsselt durchgeführt. Auch über diesen Punkt kann man streiten. Da die Backup-DVDs nur in meinem privaten Büro und meinem Bankschließfach gelagert werden, sind diese genauso gut geschützt, wie es ein Papierdokument wäre. Gegen eine Verschlüsselung spricht meiner Meinung nach die Unsicherheit, dass im Worst-Case die Daten noch zugreifbar sind. Was ist, wenn die Erben auf die Dokumente zugreifen möchten? Was ist, wenn man das Passwort vergessen hat? Oder die Verschlüsselungssoftware nicht mehr funktioniert? Dass die Medien weggeschlossen sind, reicht mir als Sicherheit aus.

## Versionierung und Änderungsverfolgung

Ein Problem ist noch nicht ganz gelöst. Es kann schnell passieren, dass man ein Dokument oder einen ganzen Ordner löscht und es gar nicht bemerkt. Ein falsches Kommando in der Kommandozeile oder einmal unaufmerksam die "Entf"-Taste gedrückt und schon ist es passiert. Jetzt haben wir zwar ein Backup der Dateien ... Aber wir merken ggf. gar nicht, dass wir dieses bräuchten. Wir können uns ja nicht jede einzelne Datei merken. Aus Versehen einen Ordner aus dem Jahr 2018 gelöscht. Das fällt uns sicherlich nicht auf.

Die Lösung ist hier einfach: Die Versionsverwaltung Git. Git ist nicht gerade ideal geeignet um Binärdateien zu verwalten, da dies mit der Zeit sehr viel Platz benötigt. Da sich unsere PDFs aber nicht ändern sollten, ist dies auch für Git kein Problem.

Mittels Git haben wir eine Änderungsverfolgung für unser komplettes Dokumentenverzeichnis. Löschen wir einen Ordner aus Versehen, sehen wir dies in Git und können entweder über das Backup oder über Git selbst den Ordner wieder herstellen. Wir haben somit also eine weitere Sicherungsstufe eingebaut.

Git wird für meine Dokumente nur lokal verwendet. Also ohne einen Server. Immer wenn ich wieder einen Schwung an Dokumenten digitalisiert und abgelegt habe, schaue ich mittels [SmartGit](https://www.syntevo.com/smartgit/) oder Git auf der Commandline (`git status`), welche Änderungen in meinem Dokumentenverzeichnis passiert sind. Sehe ich nur neu hinzugekommene Dateien ist alles gut. Sehe ich, dass Dateien gelöscht, umbenannt oder geändert wurden, schaue ich noch mal genau hin.

    [Dokumente]$ git status
    On branch master
    Changes not staged for commit:
      (use "git add/rm <file>..." to update what will be committed)
      (use "git restore <file>..." to discard changes in working directory)
        deleted:    1 Bank und Rente/xyz/2020/Steuermitteilungen/2020-08-14 Steuermitteilung_vom_14.08.2020.pdf
        modified:   "1 Bank und Rente/abc.ods"
    
    Untracked files:
      (use "git add <file>..." to include in what will be committed)
        1 Bank und Rente/xyzhh/2020-09-03 Dokument1.pdf
        ....
    
    no changes added to commit (use "git add" and/or "git commit -a")


Die Verwendung von Git würde ich als optional einstufen. Kennt man es bereits, weil man Software-Entwickler ist, dann ist es ein gutes Hilfsmittel. Hatte man mit Git noch keine Berührungspunkte, ist es etwas zu viel des Guten, sich nur für das Thema Dokumentenverwaltung in Git einzuarbeiten.

	git add *
	git commit -m "Neue Dokumente hinzugefügt"
	git status

Mehr Kommandos braucht es nicht, um eine saubere Versionsverwaltung zu haben.

---

***Randnotiz:*** Git sollte nur lokal verwendet werden. Keinesfalls die Dokumente nach Github, Codeberg & Co pushen. Aber das sollte sowieso klar sein ...

---

## Fazit

Dies war der letzte wichtige Schritt, den man sicher beherrschen sollte, bevor man mit der Digitalisierung seiner Dokumente beginnt:


1. Scannen.
2. OCR.
3. Speichern.
4. Ablegen.
5. Backup.

Fertig.

Fast... :)