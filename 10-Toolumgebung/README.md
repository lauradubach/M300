10-Toolumgebung
==
Inhalt
--
* Git Client / Git Account
* Virtual Box
* Vagrant
* Atom (Visual Studio Code)
* Reflexion

Git Client / Git Account
--
Als erstes werden wir uns einen Git Account erstellen und alles Notwendige dazu Konfigurieren.
Zuerst den Installer Herunterladen: _https://git-scm.com/downloads_
Ein GUY leitet Sie ganz einfach durch alles Notwendige. Einen Git Account können Sie ganz einfach unter:_www.github.com anlegen_.

Im Git Client erstellen wir einen Ordner in welchem wir das Repository Herunterladen können.

Im gewünschten Ordner folgenden Befehl eingeben:
_$ git clone https://github.com/mc-b/M300_ (Der Link muss natürlich Ihrem Pfad entsprechen)

Um weitere Schritte durrchzuführen können Sie dieses Glossar verwenden:

#### Glossar

| Befehle       | Bedeutung     |
| ------------- |:-------------:|
|$ git config --global user.name "<username>"  |#Account Konfigurieren  |
|$ git config --global user.email "<e-mail>"   |#Account Konfigurieren  |   
|$ git clone https://github.com/mc-b/M300      |#Repository Klonen      |
|$ git pull    / push                                |#Repository Aktualisieren|
|$ git status                                  |#Status anzeigen        |
|$ git add -A                                  |#Dateien dem Upload hintufügen|                       
|$ git commit -m "Mein Kommentar"              |#Upload commiten        |

Virtual Box
--
Nun wie gewohnt eine Virtuelle Ubuntu Maschine Installieren.
https://ubuntu.com/download/desktop

Ubuntu Version: 20.04.2.0

Vagrant
--
Vagrant ist ein Programm zur Erstellung und Verwaltung virtueller Maschinen und ermöglicht einfache Softwareverteilung.

Vagrant Anwendung herunterladen: https://www.vagrantup.com/

| Befehle       | Bedeutung     |
| ------------- |:-------------:|
|$ vagrant init ubuntu/xenial64     | #Vagrantfile erzeugen  |
|$ vagrant up --provider virtualbox  |#Virtuelle Maschine erstellen und starten  |   



Atom (Visual Studio Code)
--

Nun sollten wir einen Editor Herunterladen. Ich habe mich für Atom entschieden, da ich diesen schon kannte und besser klarkomme.

Unter: _https://atom.io/_ lässt sich die neuste Version Downloaden.

#### Extentions Installieren

Wir fügen dem Editor folgende Extentions hinzu:

* Markdown All in One
* Vagrant Extension
* vscode-pdf Extension

Jedoch können wir dies bei Atom auslassen, da bei diesem Editor schon alles integriert ist.
