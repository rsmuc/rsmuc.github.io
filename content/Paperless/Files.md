---
title: "Schritt 4: Die Dateistruktur, Dokumentenmanagementsysteme und die Ordnerstruktur"
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

Das ist für den Privathaushalt übertrieben und zum Teil sogar riskant. Ich will ja nicht zum Vollzeit-
Admin werden.

Eine Übersicht mit einer Auswahl an freien Dokumentenmanagementsystemen ist bei Wikipedia zu finden:
[Link](https://de.wikipedia.org/wiki/Dokumentenmanagement#Freie_Software)

## Tagspaces

## Tagging

## Ordnerstruktur



### Ideen
- Paginierstempel schlosser.info
https://www.schlosser.info/buero-papierlos-scanner-scanscap/

- Tags in Dateinamen aufnehmen

- Wobhin mit Dateien für die Steuererklärung: Taggen?

