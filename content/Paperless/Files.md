---
title: "Schritt 4: Organisation und Strukturierung der digitalen Dokumente."
date: 2020-09-02T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/step4.png'
tags: ["papierloses Büro", "DMS", "Dokumentenmanagement", "Ordnerstruktur", "Dateistruktur"]
toc: true
---

Wir haben nun also alle Grundlagen, um Dokumente zu digitalisieren. Es fehlt aber noch an Struktur.

## Die Dateistruktur und -benennung

### Massenabfertigung

Aller Anfang ist schwer ... Es haben sich zig Ordner mit alten Rechnungen, Kontoauszügen und
sonstigen Unterlagen angesammelt, die ich seit Jahren nicht mehr angeschaut habe. Vermutlich geht es
dir auch so. Wahrscheinlich wird man diese Dokumente auch nie wieder brauchen. Aber einfach ungesehen
vernichten? Das wollte ich nicht. Einzelne wichtige Dokumente aussortieren und nur diese scannen? 
Was ist wichtig? Was ist unwichtig? Diese Entscheidung für Dokumente zu treffen ist schwer.

Also musste eine andere praktikable Lösung her. Das Zeitaufwändige beim Scannen der Dokumente ist
ja mittlerweile nur noch das Vorbereiten der Dokumente und das Abspeichern mit einem prägnanten Dateinamen.
Der Scan selbst dauert durch den automatischen Dokumenteneinzug nicht besonders lange. Aber jede 5 oder 10
Jahre alte Rechnung und jeden alten Kontoauszug einzelnen benennen?

Nein. Hier machen wir uns zu Nutzen, dass die Dokumente grob vorsortiert in den Ordnern sind, 
wir sie vermutlich nie wieder brauchen und wir OCR haben. Die Strategie:

Alle Dokumente werden, so wie sie in den Ordnern sind, eingescannt und je Aktenordner in einer einzelnen
Datei gespeichert. Mittels OCR können wir später z.B. nach "Canyon" suchen, wenn wir die Rechnung
für das 5 Jahre alte Canyon Rennrad suchen.

Die Datei wird dann z.B. `2012-2014 Rechnungen.pdf` genannt. Oder `2010-2015 Kontoauszüge.pdf`.

Man sollte sich noch immer das ein oder andere November-Wochenende mit schlechtem Wetter hierfür
reservieren. Große Mengen zu digitalisieren ist schon eine zähe Aufgabe. Größte Motivation:
Man kann langsam aber sicher beobachten, wie sich das Büroregal leert.

### Wichtige Dokumente & Alltag

Für wichtige Dokumente und die Dokumente, die wir nun jede Woche per Post bekommen, sollten wir 
nicht mehr einfach alles in eine einzelne Datei schieben. Hier ist es angebracht, jedes Dokument
einzeln zu scannen und zu benennen.  also z.B.: `2020-09-03 Nebenkostenabrechnung 2019.pdf`.

Vor den eigentlichen Namen wird immer das Datum des Dokuments (welches auf dem Dokument steht; nicht der
Zeitpunkt der Erfassung) in [ISO 8601](https://de.wikipedia.org/wiki/ISO_8601) Schreibweise gestellt.

Der Vorteil der ISO-Schreibweise: Bei Alphabetischer Sortierung im Dateibrowser oder auf der Commandline,
stimmt die Sortierung.

Somit haben wir nun also zwei Möglichkeiten nach einer Datei zu suchen. Entweder über den Inhalt oder
über den Dateinamen.

Zum Thema "Finden von Dokumenten" wird es einen eigenen Artikel geben.

---

***Randnotiz:*** Sonderzeichen, Umlaute und Leerzeichen in Dateinamen sind nicht bei jedem beliebt.
Ich sehe da kein Problem. UTF-8 wird mittlerweile von jeder halbwegs vernünftigen Applikation
unterstützt.

---

## Dateiablage / Dokumentenmanagement / Ordnerstruktur

Damit ist nun klar, wie Dokumente selbst strukturiert und benannt werden. Aber noch nicht, wie 
die Dokumente nun abgelegt werden. In einem Dokumentenmanagmentsystem? Alle Dokumente nur in einem
Verzeichnis und wir arbeiten über die Suche? Oder ganz klassisch in einer Ordnerstruktur?

### Dokumentenmanagementsystem

Ein Dokumentenmanagementsystem ist meist eine geschlossene Applikation mit einer Datenbank, welche
Dateien vollständig in einer Datenbank indiziert, somit diese also schnell durchsuchbar macht 
und versucht automatisch oder über manuelle Zuordnung Dokumente zu sortieren und zu taggen. Häufig
findet auch eine Versionsverwaltung statt, so dass man jederzeit auf alte Versionen zurückgreifen kann.

Meist läuft ein Dokumentenmanagementsystem nicht lokal auf einem Client, sondern auf einem zentralen Server.
Viele DMS werden dann über den Webbrowser gesteuert und bedient. 

Keine Frage. Ein DMS ist mächtig und erfüllt viele Aufgaben. Aber ich bin ein Freund des KISS-Prinzips.
Keep it small an simple.

In einem Büro mit mehreren Mitarbeitern ist ein DMS unerlässlich. Aber in einem privaten Büro? Ich möchte
keinen Server pflegen, der 24/7 im Dauerbetrieb läuft. Ich möchte meine Daten nicht in ein ggf. 
proprietäres System stecken bei dem diese ggf. nicht mehr direkt zugreifbar sind. Meine Daten als Blob
in einer Datenbank? Meine Daten gespeichert in einem Blockfilesystem, welches ohne zusätzliche Tools
nicht lesbar ist?

Das ist für den Privathaushalt übertrieben und zum Teil sogar riskant. Ich will ja nicht zum Vollzeit-Admin werden.

Eine Übersicht mit einer Auswahl an freien Dokumentenmanagementsystemen ist bei Wikipedia zu finden:
[Link](https://de.wikipedia.org/wiki/Dokumentenmanagement#Freie_Software)

## Tagspaces

[Tagspaces](https://www.tagspaces.org/) bezeichnet sich als offline Lösung um Dateien und Ordner mit Farben 
und Tags zu organisieren. Tagspaces ist Open Source und steht als Community Edition zur Verfügung.

Das Interessante an Tagspaces: Die Tags werden nicht in einer zentralen Datenbank verwaltet oder gar
alle Dateien in einer zentralen Datenbank abgelegt, sondern die Tags werden im jeweiligen Dateinamen
hinterlegt.

![Tagspaces](/Paperless/pictures/tagspaces.png)

Wenn die Datei also `2020-02-22 Rechnung O2.pdf` heißt und mit den Tags "bezahlt" und "Steuer2020"
versehen werden soll, heißt die Datei hinterher `2020-02-22 Rechnung O2[bezahlt Steuer2020].pdf`.

---

***Randnotiz:*** Man kann in Tagspaces auch die "Sidecar"-Option aktivieren. Dann werden Dateien nicht
umbenannt, sondern es wird in jedem Verzeichnis ein Ordner `.ts` angelegt, welcher die Tagging-Informationen
enthält. Dies kann bei der Verwendung einer Versionsverwaltung, wie Git, interessant sein. 

---

Auch wenn ich die Grundidee von Tagspaces gut finde, besonders weil die Daten lokal bleiben und nicht
in irgendeiner Datenbank verschwinden, konnte ich mich an die Bedienung von Tagspaces
nicht wirklich gewöhnen.

## Flache Ablage

Im [Blog von Dr. Joachim Schlosser](https://www.schlosser.info/buero-papierlos-scanner-scanscap/)
bin ich auf den interessanten Ansatz gestoßen, dass man ja auch alle Dokumente flach in einem
Ordner ablegen könnte. Sortiert wird über das Datum und der Rest wird über das Datum, anschließend
wird nur mit Tags gearbeitet.

Der große Vorteil: Es geht schnell. Scannen, Datei benennen, OCR in einen einzelnen Ordner verschieben
und fertig.

Der Nachteil: Je nach Anzahl der Dokumente kann dies meiner Meinung nach unübersichtlich werden.
Damit man z.B. zusammenhängende Dokumente einer Behördenkommunikation wieder findet, müssen
die Tags sehr konsistent sein, sonst geht das Prinzip in die Hose. 

Beispiel:

    2020-01-05 KVR Anfrage Passwort Personalausweis.pdf
    [100 andere Dokumente]
    2020-02-22 KVR Neues Passwort Personalausweis.pdf
    2020-02-23 KVR Fehlerhaftes Passwort Personalausweis.pdf
    [100 andere Dokumente]
    2020-04-23 Kreisverwaltung Reset Passwort Personalausweis.pdf
    2020-04-24 Kreisverwaltung Bestätigung Reset Passwort Personalausweis.pdf
    
    
Ich habe also aus Versehen beim Scannen das Dokument nicht mehr mit dem Tag "KVR" versehen, sondern
mit Kreisverwaltung, weil ich nicht in Erinnerung hatte, dass ich eigentlich KVR verwende.
Will ich nun den gesamten Verlauf wieder zusammen suchen, habe ich ein Problem.    

Tagspaces würde das Problem lösen, da es die Tags konsistent hält.

## Ordnerstruktur

Aber was spricht eigentlich gegen den Klassiker? Warum nicht einfach eine Ordnerstruktur aufbauen?

Wir müssen die Dokumente wieder händisch einsortieren, was uns Zeit kostet. Aber dies lässt sich
technisch lösen. Dazu wird es ein eigenes Kapitel zum Thema Automatisierung geben.

Ich lege also meine Dokumente in einer einfachen Ordnerstruktur ab. Diese ist natürlich für jeden
individuell. Aber vom Prinzip sieht es bei mir so aus:

    01 Banken:
        --> HVB
        --> Sparkasse
            --> 2018
            --> 2019
            --> 2020
                --> Kontoauszüge
                --> Verträge
                    --> 2020-03-03 Sparbuch.pdf
    02 Krankenkasse
        --> 2018
        --> 2019
        --> 2020
            --> 2020-02-02 Rechnung.pdf 

So kann ich sicher sein, dass sämtliche Kommunikation bzgl. meiner Verträge mit der Sparkasse
im entsprechenden Ordner ist.

## Tagging

Was aber nun, wenn wir z.B. eine Jahressteuerbescheinigung von der HVB bekommen haben? Erst mal ganz
einfach. Die kommt in den "HVB" Ordner für das Jahr "2020" mit dem Unterordner "Sonstiges".

Im nächsten Jahr bei der Steuererklärung müssen wir dann aber alle relevanten Dokumente wieder händisch
zusammen suchen. Alternativ könnten wir auch eine Kopie des Dokuments in den HVB Ordner legen und 
eine andere Kopie des Dokuments in den Ordner "09 Steuererklärung/2020". Doppelte Datenhaltung ist
aber nie die Lösung.

Hierfür haben wir die Lösung auch schon in der Hand. Tags. Das Dokument wird also 
`2020-08-05 HVB Jahressteuerbescheinigung [Steuer2019]` benannt. Und auch die Spendenbescheinigung
kommt zwar in den Ordner "BRK", aber erhält zusätzlich den Tag [Steuer2019].

Mit Tags als Querverweise sollte man sparsam sein. Bei mir gibt es nur den Tag für die Steuer.
Alle anderen Dokumente sind immer nur einem Thema zugeordnet.