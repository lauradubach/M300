LB02
==

In den nachfolgenden Zeilen werde ich alles notieren was ich zu den Themen Container, Docker, Kubernetes und über die Sicherheit dazu gelernt habe.

Definition Container
--
Container sind eine Virtualisierungstechnik im Computerumfeld, die Anwendungen inklusive ihrer Laufzeitumgebungen voneinander trennt. Im Gegensatz zu einer virtuellen Maschine beinhalten Container kein eigenes Betriebssystem, sondern verwenden das des Systems, auf dem sie installiert sind. Container haben verschiedene Merkmale wie zum Beispiel, dass sie in einer Sekunde gestartet und gestoppt werden können, sie teilen sich Resourcen mit dem Host-Betriebssystem, sie sind portierbar und Cloud-Ready.

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Fotos/Container.PNG" width="500" height="350">

Definition Docker
--
Docker ist eine Software, welche die Container-Virtualisierung von Anwendungen ermöglicht. Anwendungen können inklusive ihrer Abhängigkeiten in ein Image gepackt werden. Mittels einer speziellen Engine kann die so verpackte Anwendung dann in einem Docker Container ausgeführt werden.

#### Vorteile

* Die gute Skalierbarkeit durch die Nutzung von vielen weiteren container
* Das schnelle starten und herunterfahren
* Durch die einfache Verwaltung von Containern

#### Die wichtigsten Komponenten sind:

* Docker Daemon
* Docker Client
* Images
* Container
* Docker Registry

**Docker Daemon**

Dieser erstellt, überwacht und führt Container aus. Er baut und speichert auch Images. Er wird mit dem Host-Betriebssystem gestartet.

**Docker Client**

Er wird über die Kommandozeile (CLI) gestartet. Er kommuniziert über HTTP so ist es einfach Verbindungen zu Docker Daemons herzustellen.

**Images**

Dies sind Umgebungen die man als Container starten kann, man kann sie nicht verändern, sondern nur neue erstellen. Ein Image besteht aus einem Namen und der version.

**Container**

Dies sind die ausgeführten Images. Hier kann man veränderungen vornehmen, es werden jedoch nur die Änderungen zum originalen Image abgespeichert.

**Docker Registry**

Hier werden die Images abgelegt und verteilt. Docker-Hub ist die Standart-Registry indem sich viele Images befinden.

Testfälle
--
Um auf meinen Server Zugriff zu erhalten gehe ich wie folgt vor:
1. Im cmd über ssh eine Verbindung herstellen: _$ssh ubuntu@IP_
2. Nun das korrekte Passwort eingeben

#### Docker-Container kombinieren

1. ``$docker run --name osticket_mysql -d -e MYSQL_ROOT_PASSWORD=secret \
 -e MYSQL_USER=osticket -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=osticket mariadb``

2. ``$docker run --name osticket -d --link osticket_mysql:mysql -p 3030:80 osticket/osticket``

Nun sollte unter folgender URL _IP:3030_ dieser Output auftauchen:

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Fotos/Container%20Kominieren.PNG" width="500" height="300">

#### Bestehende Container als Backend, Desktop-App als Frontend einsetzen

* Als erstes erstellen wir ein Dockerfile: _$docker build -t "Name"_
* Nun erstellen wir den Container welcher auf Port 8080 hört: _$docker run -dit --name "Name" -p 8080:80 "Name"_

Wenn man nun die IP-Adresse mit dem Port eingibt sollte man folgendes Ergebniss erhalten:

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Fotos/It%20works.PNG" width="400" height="200">

#### Volumes zur persistenten Datenablage eingerichtet


Glossar
--

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

Das Überwachen und kontrollieren von laufenden Containern ist sehr wichtig. Man kann hierfür gute Monitoring-Lösungen verwenden

#### Sicherheits Aspekte

**Kernel Exploits**

Der Kernel wird von allen Containern und dem Host verwendet, somit ist die Angriffsstelle mit deutlich mehr Auswirkung verbunden.

**Denial-of-Service-(DoS-)Angriffe**

Da sich alle Container die Kernel Ressourcen teilen, könnte ein Container den Zugriff auf bestimmte Ressourcen ganz für sich beanspruchen oder andere Container "verhungern" lassen.

**Container-Breakouts**

Wenn man im Container ein root ist, wird man auch root auf dem Host, dies ist sehr problematisch, da ein Angreifer der Zugriff auf einen Container erhält, auch Zugriff auf den Host bekommen kann.  

**Vergiftete Images**

Wenn man ein Image herunterlädt, kann man nicht wissen ob dies vielleicht manipuliert wurde. So kann man den Host und die eigenen Daten gefährden.

**Verratene Geheimnisse**

Wenn man auf einen Container oder eine Datenbank zugreiffen will benötigt man zb einen API-Schlüssel oder ein Benutzername und ein Passwort. Ein Angreifer könnte dies herausfinden und auf das System zugreiffen.

**Least Privilege**

Jeder Prozess und Container sollte nur mit so viel Zugriffsrechten und Ressourcen laufen, wie er gerade braucht, um seine Aufgaben zu erfüllen.

* Sicherstellen, dass Prozesse in Containern nicht als root laufen
* Dateisysteme schreibgeschützt einsetzen
* Kernel Aufrufe einschränken
* Ressourcen begrenzen

Beispiele
--

#### Berechtigungen eingrenzen
`` $ RUN groupadd -r user_grp && useradd -r -g user_grp user
    $ USER user``

#### Speicher begrenzen

``$ docker run -m 128m --memory-swap 128m amouat/stress stress --vm 1 --vm-bytes 127m -t 5s``

#### Neustarts begrenzen

``$ docker run -d --restart=on-failure:10 my-flaky-image``

#### Zugriffe auf die Dateisysteme begrenzen

`` $ docker run --read-only ubuntu touch x``

#### Capabilities einschränken

``$ docker run --cap-drop all --cap-add CHOWN ubuntu chown 100 /tmp``

#### Ressourcen einschränken

``$ docker run --ulimit cpu=12:14 amouat/stress stress --cpu 1_``



#### 3 Aspekte der Container Absicherung

1. Ein Passwort erstellen
2. Host Ordner Zugriff einschränken (Least Privilege)
3. Einen Container als none root anlegen/erstellen

Testfälle
--

#### Service Überwachung

Mit folgendem Befehl kann man eine einfache Monitoring-Lösung einrichten:
_$docker run -d --name cadvisor -v /:/rootfs:ro -v /var/run:/var/run:rw -v /sys:/sys:ro -v /var/lib/docker/:/var/lib/docker:ro -p 2020:8080 google/cadvisor:latest_

Nun sollte man unter folgendem Link auf das Monitoring Tool kommen: _IP:2020/containers/_

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Fotos/Monitoring%20Tool.PNG" width="500" height="350">

#### Aktive Benachrichtigung einrichten

Kubernetes
--

Kubernetes ist ein Open-Source-System zur Automatisierung der Bereitstellung, Skalierung und Verwaltung von Container-Anwendungen.

#### Wichtige Merkmale

* Immutable statt Mutable.
* Deklarative statt Imperative Konfiguration.
* Selbstheilende Systeme - Neustart bei Absturz.
* Skalieren der Services durch Änderung der Deklaration.
* Entkoppelte APIs – LoadBalancer / Ingress (Reverse Proxy).
* Anwendungsorientiertes statt Technik Denken.
* Abstraktion der Infrastruktur statt in Rechnern Denken.

#### Objekte

1. **Pod** -> Ein Pod repräsentiert eine Gruppe von Anwendungs-Containern und Volumes, die in der gleichen Ausführungsumgebung laufen.
2. **ReplicaSet** -> ReplicaSets bestimmen wieviele Exemplare eines Pods laufen und stellen sicher, dass die angeforderte Menge auch verfügbar ist.
3. **Deployment** -> Deployments erweitern ReplicaSets um deklarative Updates von Container Images.
4. **Service** -> Ein Service steuert den Zugriff auf einen Pod.
5. **Ingress** -> Ähnlich einem Reverse Proxy ermöglicht ein Ingress den Zugriff auf einen Service über einen URL.

Kubernetes Cluster
--

<img src="https://github.com/lauradubach/M300/blob/main/LB02/Fotos/Kubernetes.PNG" width="500" height="350">

Bei einem Cluster wird ein Kubernetes Master und mehrere Worker erzeugt. Diese Umgebung eignet sich zur Demonstration einer Verteilten Umgebung.

#### Konfiguration

``master:
  count: 1
  cpus: 2
  memory: 5120
worker:
  count: 2``

Es wird ein Master und zwei Worker Nodes erstellt. Der Master und die Worker Nodes werden während der Installation automatisch miteinander gejoint.

``use_dhcp: false  
Fixe IP Adressen mit welchen die IP fuer Master und Worker beginnen sollen
ip:
  master:   192.168.137.100
  worker:   192.168.137.111
  Netzwerk "private_network" fuer Host-only Netzwerk, "public_network" fuer Bridged Netzwerke
net:
  network_type: private_network``

Die restlichen Standardeinstellungen wie Host-only Netzwerk mit fixen IP-Adressen kann 1:1 verwendet werden.

Lernvortschritt
--

Auch in diesem Abschnitt, kannte ich voher nichts. Am Anfang hatte ich Mühe mich einzulesen und alles zu verstehen, jedoch ging es nach ein paar Übungen scho ganz gut. Nun weiss ich was ein Container ist, was Docker ist, ich weiss wie man ein Container macht und ein Dockerfile erstellt, ich weiss auch wie man ein Image erstellt. In der Theorie habe ich sehr viel über die Sicherheitsaspekte gelernt und auch Kubernetes ein bisschen kennengelernt. Für mich war dieses Modul sehr interessant und eine grosse Wissensbereicherung.
