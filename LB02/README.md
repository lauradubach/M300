LB02
==

In den nachfolgenden Zeilen werde ich alles notieren was ich zu den Themen Container, Docker, Kubernetes und über die Sicherheit dazu gelernt habe.

Definition Container
--
Container sind eine Virtualisierungstechnik im Computerumfeld, die Anwendungen inklusive ihrer Laufzeitumgebungen voneinander trennt. Im Gegensatz zu einer virtuellen Maschine beinhalten Container kein eigenes Betriebssystem, sondern verwenden das des Systems, auf dem sie installiert sind. Container haben verschiedene Merkmale wie zum Beispiel, dass sie in einer Sekunde gestartet und gestoppt werden können, sie teilen sich Resourcen mit dem Host-Betriebssystem, sie sind portierbar und Cloud-Ready.

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Container.PNG" width="500" height="350">

Definition Docker
--
Docker ist eine Software, welche die Container-Virtualisierung von Anwendungen ermöglicht. Anwendungen können inklusive ihrer Abhängigkeiten in ein Image gepackt werden. Mittels einer speziellen Engine kann die so verpackte Anwendung dann in einem Docker Container ausgeführt werden.

#### Vorteile

* Die gute Skalierbarkeit durch die Nutzung von vielen weiteren container
* Das schnelle starten und herunterfahren
* Durch die einfache Verwaltung von Containern

#### Die wichtigsten Komponente sind:

* Docker Daemon
* Docker Client
* Images
* Container
* Docker Registry

#### Docker Daemon
Dieser erstellt, überwacht und führt Container aus. Er baut und speichert auch Images. Er wird mit dem Host-Betriebssystem gestartet.

#### Docker Client

Er wird über die Kommandozeile (CLI) gestartet. Er kommuniziert über HTTP so ist es einfach Verbindungen zu Docker Daemons herzustellen.

#### Images

Dies sind Umgebungen die man als Container starten kann, man kann sie nicht verändern, sondern nur neue erstellen. Ein Image besteht aus einem Namen und der version.

#### Container

Dies sind die ausgeführten Images. Hier kann man veränderungen vornehmen, es werden jedoch nur die Änderungen zum originalen Image abgespeichert.

#### Docker Registry

Hier werden die Images abgelegt und verteilt. Docker-Hub ist die Standart-Registry indem sich viele Images befinden.

Testfälle
--
Um auf meinen Server Zugriff zu erhalten gehen ich wie folgt vor:
1. Im cmd über ssh eine verbindung herstellen $ssh ubuntu@IP
2. Nun das korrekte Passwort eingeben



#### Glossar

| Befehle       | Bedeutung     |
| ------------- |:-------------:|
|$docker build -t "Name" .  |#Image von Dockerfile erstellen  |
|$docker ps   |#alle container anzeigen die gestartet wurden  |  
|$docker run | #zum starten neuer Container |
|$docker run -dit --name "Name" -p 8080:80 "Name" |#Container wird erstellt und hört auf Port 8080 |
|$docker stop/start/remove "Name/ID" |#Docker starten,stoppen, löschen |
|$docker logs "Name/ID" |#Output anschauen |
|$docker images | #gibt eine Liste lokaler Images aus |
|$docker rm/rmi | #Entfernt Container / Entfernt Image |
|$docker logs | #Gibt die logs eines Containers aus |

Sicherheit
--

#### 3 Aspekte der Container Absicherung

1. Ein Passwort einstellen
2. Host Ordner Zugriff einschränken
3. Einen Container als none root anlegen/erstellen

Lernvortschritt
--
