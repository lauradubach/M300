LB02
==

In den nachfolgenden Zeilen werde ich alles notieren was ich zu den Themen Container, Docker, Kubernetes und Sicherheit gelernt habe.

Definition Container
--
Container sind eine Virtualisierungstechnik im Computerumfeld, die Anwendungen inklusive ihrer Laufzeitumgebungen voneinander trennt. Im Gegensatz zu einer virtuellen Maschine beinhalten Container kein eigenes Betriebssystem, sondern verwenden das des Systems, auf dem sie installiert sind. Container haben verschiedene Merkmale wie zum Beispiel, dass sie in einer Sekunde gestartet und gestoppt werden können, sie teilen sich Resourcen mit dem Host-Betriebssystem, sie sind portierbar und Cloud-Ready.

<img src="LB02/Container.png.PNG" width="500" height="350">

#### Glossar

| Befehle       | Bedeutung     |
| ------------- |:-------------:|
|$docker build -t "Name" .  |#Image von Dockerfile erstellen  |
|$docker ps   |#alle container anzeigen die gestartet wurden  |   
|$docker run -dit --name "Name" -p 8080:80 "Name" |#Container wird erstellt und hört auf Port 8080 |
|$docker stop/start/remove "Name/ID" |#Docker starten,stoppen, löschen |
|$docker logs "Name/ID" |#Output anschauen |
