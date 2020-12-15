---
title: "Backup: Kontakte und Kalender"
sub: "Manchmal geht einfach alles schief"
date: 2020-12-14T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/title-crash.jpg'
tags: ["papierloses Büro", "Backup", "Kontakte", "Kalender"]
toc: true
-

## Die Ausgangssituation

Seit Jahren bin ich nun zufriedener Kunde bei mailbox.org und nutze dies nicht nur als Mailanbieter, sondern habe dort auch mein Adressbuch als auch meinen Kalender.

Es war der Juni 2018, in der sorglosen Prä-Corona-Zeit, auf dem Weg in ein Urlaubswochenende. Mein Smartphone war der Meinung, dass es mitten auf der Autobahn eine gute Idee ist abzustürzen, während DAVx gerade meine Kontakte synchronisiert. Nach einem Neustart: Das Adressbuch ist leer. DAVx versucht erneut zu synchronisieren. Es sind nur noch 3 unvollständige Einträge im Adressbuch. 330 Kontakte weg.

Dank Synchronisation vermutlich auch auf dem Server gelöscht. Dank aktivierter 2FA mit dem Yubikey ein Einloggen auf dem Webinterface vom Smartphone aus nicht möglich. Ein guter Start ins Wochenende.


## Vdirsyncer

Mailbox.org und vermutlich auch die meisten anderen Anbieter führen kein Backup von Kalender und Adressbuch durch. Aber es gibt Abhilfe in Form des Tools [vdirsyncer](https://github.com/pimutils/vdirsyncer). Vdirsyncer kann eigentlich mehr als nur ein Backup erstellen. Das Tool kann Kalender und Kontakte vollständig zur Offline-Nutzung in beide Richtungen synchronisieren. Uns interessiert hauptsächlich der Weg vom (mailbox.org-)Server zu unserem Notebook.

### Die Installation

Viele Wege führen nach Rom. In diesem Fall sind sie zum Glück alle nicht besonders steinig. 

Ich verwende als Linux-Distribution Manjaro, welche auf ArchLinux basiert und auf das AUR von Arch zugreifen kann. Im AUR ist vdirsyncer vorhanden und gut gepflegt und kann somit einfach installiert werden. Auch für Debian und Ubuntu stehen Pakete zur Verfügung und können einfach installiert werden: [Offizielle Dokumentation](https://vdirsyncer.pimutils.org/en/stable/installation.html)

Alle anderen können auch mit PIP arbeiten. Ein einfaches `pip install --user vdirsyncer` sollte ausreichend sein.

### Die Konfiguration

Bis hierhin war es noch einfach. Die Konfiguration erfolgt in der Datei `~/.vdirsyncer/config`. Also legen wir diese Datei an. 

Eine detaillierte Beschreibung der Konfigurationsdatei findet sich in der Dokumentation des Tools: [Link zur Dokumentation](https://vdirsyncer.pimutils.org/en/stable/tutorial.html)

Mit diesem Beispiel werden sowohl die Kontakte als auch der Kalender von Mailbox.org synchronisiert. Das Passwort wird nicht direkt in der Konfigurationsdatei gespeichert, sondern über das secret-tool abgerufen. Details dazu gleich.


    [general]
    status_path = "~/.vdirsyncer/status/"
	
	############   
	# Kontakte
	############
		
    [pair example_contacts]
    
    a = "example_contacts_local"
    b = "example_contacts_remote"
    collections = ["from a", "from b"]    
    metadata = ["displayname"]
    conflict_resolution = "b wins"
    
    [storage example_contacts_local]
    type = "filesystem"
    path = "~/.vdirsyncer/contacts/"
    fileext = ".vcf"
    
    [storage example_contacts_remote]
    type = "carddav"
    url = "https://dav.mailbox.org/caldav/"
    username = "example@mailbox.org"
    password.fetch = ["command", "secret-tool", "lookup", "mailbox", "mailbox"]
	   
	###########
	# Kalender
	###########
	
    [pair example_calendar]
    a = "example_calendar_local"
    b = "example_calendar_remote"
    collections = ["from a", "from b"]
    metadata = ["displayname", "color"]
    conflict_resolution = "b wins"
	
    [storage example_calendar_local]
    type = "filesystem"
    path = "~/.vdirsyncer/calendars/"
    fileext = ".ics"
	
    [storage example_calendar_remote]
    type = "caldav"
    url = "https://dav.mailbox.org/caldav/"
    username = "example@mailbox.org"
    password.fetch = ["command", "secret-tool", "lookup", "mailbox", "mailbox"]

Die hier genannte Beispielkonfiguration kann so weit 1:1 übernommen werden. Nur "example" muss durch den jeweiligen Username bei Mailbox.org ersetzt werden.

Was ist nun mit dem Passwort. Die einfache Variante, statt dem im Beispiel genannte 'password.fetch ...' wäre der Eintrag:

	password = "asdf"

Ich bin allerdings kein großer Fan von Klartext-Passwörtern in Konfigurationsdateien. Faktisch würde dies kein echtes Problem darstellen, wenn das komplette Home-Verzeichnis oder die komplette Partition verschlüsselt ist. Denn kommt ein potenzieller Angreifer an der Verschlüsselung vorbei, z. B. weil er an ein laufendes System kommt ohne gesperrten Bildschirmschoner, hilft auch das secret-tool nicht mehr. Sicherer wäre nur, bei jeder Synchronisation das Passwort händisch einzugeben. Aber übertreiben wir es mal nicht.

Also speichern wir nun das Passwort mit dem secret-tool im Keystore: 

	secret-tool store --label="example" mailbox mailbox 

Anschließend geben wir das Passwort ein und fertig.

Zum Test können wir uns das Passwort nun auch auf der Kommandline ausgeben lassen:

	secret-tool lookup mailbox mailbox

So nun wird es ernst. Vor dem ersten Synchronisieren habe ich den Kalender und auch alle meine Kontakte über das Webinterface von Mailbox.org einmalig exportiert. Sicher ist sicher.

Starten wir nun also die Synchronisation:

	vdirsyncer discover && vdirsyncer metasync && vdirsyncer sync

Fertig. 

Nun liegen alle Kontakte und Kalender im Verzeichnis ~/.vdirsyncer. Prinzipiell können sie auch dort editiert und wieder zurück synchronisiert werden.

Da der Aufruf ein wenig sperrig ist, habe ich ihn bei mir in ein einfaches, einzeiliges Script gepackt. 

## Versionsverwaltung mit GIT

Es muss nicht immer ganz so schlimm kommen wie in meiner einleitenden Erfahrung. Einfach nur aus Versehen einen einzelnen Kontakt auf dem Smartphone gelöscht oder das Geburtsdatum verändert und versehentlich gespeichert: Dank Synchronisation sind die Daten futsch. Dank Backup erst mal kein Problem. Aber wie bekommt man überhaupt mit, dass man aus Versehen das Geburtsdatum geändert hat. Die Antwort lautet hier wieder: Git.

Zu Git habe ich im letzten Backup-Artikel schon mal ein wenig geschrieben: [Hier gehts zum Artikel](https://write.tchncs.de/~/Paperless/schritt-5-das-backup). Für die Kontakte und Kalender können wir genauso vorgehen. Das Verzeichnis vom vdirsyncer wird einfach in Git aufgenommen und alle Änderungen sind in Zukunft zu sehen. Ein kurzer Blick: Oh da ist ja ein neuer Geburtstag eingetragen und hier habe ich drei Kontakte gelöscht. Wollte ich das wirklich?

Wenn ja: git commit und gut ist

Wenn nein: Zurück zur letzten Version

## Wenn alle Stricke reißen

Alles, was irgendwie veränderlich ist, kann auch zerstört werden. Ein böser böser Trojaner, der unsere vcards verändert, mit dem mailbox.org Server synchronisiert und unser lokales Git zerstört. Ok nicht sehr wahrscheinlich. Trotzdem brenne ich bei meinen monatlichen Dokumenten-Backups einfach das .vdirsyncer Verzeichnis mit auf meine Dokumenten DVD und bunkere diese DVDs regelmäßig in meinem Bankschließfach. Sieh auch: [Backup-Artikel](https://write.tchncs.de/%7E/Paperless/schritt-5-das-backup) 

Etwas paranoid ... Aber sicher.

## Das Ende der Geschichte

Am Ende des trotz alledem schönen Wochenendes, welches jedoch tatsächlich immer wieder von den Gedanken und der Unsicherheit bezüglich der verlorenen Kontakte überschattet war: Notebook eingeschaltet und auf dem Webinterface von mailbox.org angemeldet. Schnell in die Kontakte gewechselt. Puhh noch alle Kontakte vorhanden. Zur Sicherheit ein händischer Export über das Webinterface gemacht, die Synchronisation auf dem Smartphone neu eingerichtet und alles war wieder gut. 

In Zukunft: Ein monatlich automatisiertes Backup mit Versionsverwaltung in GIT, damit so etwas nicht mehr vorkommt.
