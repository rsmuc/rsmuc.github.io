---
title: "Blog mittels Hugo und Github Pages erstellen"
date: 2020-08-27T22:25:08+02:00
draft: true
toc: true
disable_share: true
tags: ["Blog", "Hugo", "Github"]
---

### Warum Github Pages und Hugo?

Da der Blog hier nur ein kleines Hobby-Projekt nebenbei ist und nie eine besonders
große Reichweite erlangen wird, war ich nicht bereit hierfür Geld auszugeben. Es gibt
einige Webseiten im Internet, wie <https://wordpress.com> bei denen man kostenlos
Blogs führen kann. Aber da am Ende des Tages eben doch selten etwas wirklich kostenlos ist,
bezahlt man dort entweder damit, dass dort Werbung eingeblendet wird oder dass massig
Tracker eingebunden werden. Dies war also keine Option.

Das Projekt war also bereits gescheitert, bevor ich es überhaupt begonnen hatte. Zufällig
bin ich dann letztens über Github Pages gestolpert: <https://pages.github.com/>. Dort können
statische Webseiten gehostet werden. Also ohne Wordpress & Co im Hintergrund. Und da ich
sowieso schon Github nutze, habe ich mir das ganze angesehen.

Out-of-the-box können Seiten dort bereits mit Markdown geschrieben werden. Nach etwas
Recherche bin ich dann noch auf "Hugo" gestoßen: <https://gohugo.io/>.
Hugo ist ein Framework zum Generieren von statischen Webseiten. Das Ergebnis sieht man
ja hier.

### Github Pages anlegen

Die Quickstart-Beschreibung für "User or organization site" direkt auf <https://pages.github.com/> erklärt alles notwendige.
Dies werde ich hier nicht nochmal wiederholen.

Hat alles funktioniert sieht man also beim Zugriff auf die eigene Seite ein "Hello World".

Nun müssen wir noch ein paar Einstellungen vornehmen, damit später das Zusammenspiel mit Hugo klappt:

* Auf github.com einloggen und das Pages Repository öffnen
* Auf "Settings" gehen
* Dort auf der Seite ganz nach unten zu "Github Pages scrollen"
* Nun muss die "Source" angepasst werden. Diese sollte auf dem Master-Branch in den "docs"-Ordner zeigen.

![Einstellungen füt Github Pages](/blog/github-pages.png)
(Achtung im Screenshot ist nicht der Master-Branch ausgewählt, sondern "Test".)

Jetzt geht es erst mal mit Hugo weiter. 


### Hugo

[Hugo](https://gohugo.io/) wird lokal auf dem eigenen Rechner installiert und generiert dann die
statischen HTML-Seiten. Die fertigen HTML-Seiten werden dann auf Github veröffentlicht.

Die Installation von Hugo ist unter Manjaro wieder denkbar einfach. Es existiert im offiziellen
Repository, kann also mittels Pamac & Co installiert werden.

![Hugo Pamac](/blog/hugo-pamac.png)

Auch für Hugo gibt es wieder einen guten Quickstart Guideline: <https://gohugo.io/getting-started/quick-start/>
Diesen kann man grundsätzlich vollständig befolgen.

Man sollte jedoch noch in seine config.toml folgendes aufnehmen:

    publishdir = "docs/"
    
Dann werden die statischen HTML-Seiten direkt nach docs/ generiert und somit liegen sie gleich
an der richtigen Stelle.


### Mit Hugo und Github Pages arbeiten

Wie wird nun also ein neuer Blog-Artikel erstellt:

* Neue Seite erstellen:

"hugo new Paperless/Test.md"

* Das Test.md File bearbeiten, den Artikel schreiben und den Status auf "draft: false" setzen

* Den lokalen Testserver starten, um das Ergebnis zu kontrollieren:

    "hugo server"

* Sind wir mit dem Ergebnis zufrieden, werden die HTML Files generiert:
    
    HUGO_ENV=production hugo

* Nun alle Files zu Github hinzufügen:
    
    git add *
    
* Commiten:
    
    git commit -m "inhalt hinzugefuegt"
    
* Und zu Github pushen:
    
    git push
    
Nun sollte der neue Blog Artikel veröffentlicht sein.

Mehr Details zur config.toml könnt ihr auch direkt im Github-Repository dieser Seite direkt live
sehen.


### Warum die Kombination Spaß macht

* Sowohl die Konfiguration, der Inhalt (als Markdown Files) und das Ergebnis sind in Git(hub) versioniert
* Die einzelnen Artikel können schnell und einfach in Markdown geschrieben werden
* Das Angebot von Github ist kostenlos, Hugo ist OSS
* Keine versteckten Tracker
* Keine große, schwer zu wartende Infrastruktur und Plugins (wie z.B. bei Wordpress) notwendig
* Tolle fertige Themes
* Einfach und schnell in der Bedienung, wenn man sich mal eingearbeitet hat