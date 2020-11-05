---
title: "Fotos: Negative digitalisieren"
sub: "Und mit Digikam unter Linux nachbearbeiten"
date: 2020-09-08T17:24:41+02:00
draft: true
featured_image: 'Paperless/titlepics/fotos1.jpg'
tags: ["papierloses Büro", "JPEG", "Fotos", "Digitalisierung", "Negative", "Digikam"]
toc: true
---

## Negative digitalisieren

Durchwühlt man seine analoge Fotosammlung, stößt man unweigerlich auch auf Negative. Bei mir waren nicht für alle Fotos noch die Negative und nicht für alle Negative noch die Fotoabzüge verfügbar. Fotos digitalisieren können wir mit dem Dokumentenscanner, wie ich schon im letzten Artikel beschrieben habe. Für Negative ist dies nicht möglich.

### Scanner

Für relativ kleines Geld (~80 €) sind Dia- und Negativ-Scanner zu haben. Ich habe mich für ein Gerät von der Firma DIGITNOW! verfügbar. Der Scanner selbst ist auch ohne PC verwendbar und somit komplett Betriebssystem unabhängig. Es gibt auch deutlich höherpreisige Geräte, bei mir war allerdings mit 80 € die Schmerzgrenze erreicht. Auch mit einem Flachbettscanner mit Durchlichtungseinheit wäre ein Scannen von Negativen möglich. Allerdings war dies zu teuer, zu langsam und zu groß.

 ![Negativ Scanner](6157) 

Die Fotos beim Negativ-Scanner werden auf einer SD-Karte oder dem internen Speicher des Scanners abgelegt. Der interne Speicher ist 128 MB und damit erst mal ausreichend. Die Stromversorgung des Scanners erfolgt per USB über das mitgelieferte Netzteil oder man verwendet einen USB-Port eines PCs oder Notebooks. Zum Übertragen der Daten kann man dann vom Scan-Modus in den USB-Modus des Geräts wechseln. Der Scanner wird dann als "USB-Stick" erkannt und die fertigen JPEGs können vom Gerät kopiert werden.

### Workflow

Zum eigentlichen Scannen schiebt man einfach das Negativ durch den passenden beiliegenden Adapter, richtet das Negativ aus und drückt den Scan-Knopf. Anschließend das Negativ um ein Foto weiter schieben und wieder den Scan-Knopf drücken. Damit lässt sich ein Film relativ schnell digitalisieren. Pro Foto braucht man nur wenige Sekunden und ist somit auch nicht langsamer als bei Fotos mit dem Dokumentenscanner.

Problematisch ist allerdings Staub und sonstige Verschmutzungen. Man sollte drauf achten, dass die Negative von Anfang an möglichst staubfrei sind. Ansonsten hat man auf dem Foto hinterher die entsprechenden Artefakte. Noch unangenehmer: Der Staub setzt sich auch im Gerät fest und entsprechend hat man dann die Artefakte auf jedem Foto. Man sollte also immer wieder prüfen, dass keine Verschmutzungen auf den Fotos sind und das Gerät regelmäßig reinigen. Die beigelegte Reinigungsbürste halte ich für ziemlich ungeeignet. Etwas besser hat es mit einem Brillenputztuch, welches ich um einen dünnen Stift gewickelt habe, funktioniert. Richtig schön ist dies jedoch nicht. Schade, dass man das Gerät zum Reinigen nicht einfach öffnen kann.

### Weitere Einstellungen

Neben dem Scan-Modus, gibt es noch weitere Modi und Einstellungen für den Scanner. Diese erreicht man mittels der Pfeiltasten. So kann man die erfassten Fotos im Betrachtungsmodus ansehen oder, wie bereits beschrieben, im USB-Modus vom Scanner direkt auf einen Rechner kopieren. Auch ein direktes Spiegeln oder Rotieren des erfassten Bildes ist möglich. Dies mache ich jedoch nicht auf dem Gerät, sondern später in Digikam.

Im Menü "Film", kann man die Art des Films auswählen. Also ob man ein Negativ erfassen will oder ein Dia. Zudem kann dort das Format des jeweiligen Films (z.B. 135mm) angegeben werden.

Im Menü "Resolution", kann die Auflösung eingestellt werden: 14 oder 22 Megapixel. Da der Scanner allerdings nur einen 14 Megapixel Sensor hat, wird bei 22 Megapixel interpoliert. Dies führt also zu keiner besseren Bildqualität, sondern nur zu einer größeren Datei. Die Angaben bei dem ein oder anderen großen Internethändler sind hier etwas schwammig. Mal ist von 22 Megapixeln, mal von 16 und dann wieder von 14 Megapixeln die Rede. Hier also bei der Bestellung aufpassen, dass man keine böse Überraschung erlebt.



### Nacharbeit

Im Vergleich zwischen einem eingescannten Bild und einem eingescannten Negativ zeigen sich farblich einige Unterschiede, wie der Vergleich zeigt.

![Negativ vs Fotoscan](6084)
*(links Foto-Scan - rechts Negativ-Scan)*
 
Der deutlich zu sehende Blaustich lässt sich per Software jedoch sehr leicht korrigieren. Ich verwende zum Verwalten und auch Bearbeiten meiner Fotosammlung "[Digikam](https://www.digikam.org/)", welches in jeder Distribution enthalten sein sollte. Alternativ kann man die aktuelle Version auch als AppImage von der Webseite des Projektes herunterladen oder als Flatpak beziehen: [Flathub](https://flathub.org/apps/details/org.kde.digikam).

Zum Korrigieren des Blaustichs:

	DigiKam --> Image Editor --> Auto-Correction --> Equalize

Schon sieht das Ergebnis deutlich besser aus. Zu Digikam selbst, gibt es später noch einen eigenen Artikel.

![Autocorrection - Equalize](6085) 
*(links vorher - rechts hinterher)*
 
Das Endergebnis zwischen eingescanntem entwickelten analogen Foto und eingescanntem Negativ ist am Ende sehr ähnlich.

Alles im allem erreicht man schnelle und akzeptable Ergebnisse für relativ kleines Geld. Zum Konservieren von Erinnerungen ist es allemal ausreichend. Man digitalisiert ja keine Kunstwerke, sondern Erinnerungen an die Kindheit, die Eltern und die Großeltern. Wer fehlerfreie Scans und eine bessere Qualität will, muss entsprechend mehr in einen höherwertigen Scanner investieren oder gleich einen Dienstleister beauftragen.


---

***Hinweis:***

Beim Scannen von Negativen muss das Fotos häufig hinterher gespiegelt werden.

Auch dies ist in DigiKam möglich:

	Image Editor --> Toolbar --> Transform --> Flip Horizontal

---