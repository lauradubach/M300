10-Toolumgebung
==
Inhalt
--
* Git Account
* Git Client
* Virtual Box
* Vagrant
* Atom (Visual Studio Code)
* Reflexion

Git Account
--
Als erstes werden wir uns einen Git Account erstellen und alles Notwendige dazu Konfigurieren. Dieser Account dient uns als Cloud-Speicher für die Dokumentation.
* Ganz einfach unter www.github.com einen Account erstellen.
* Nun die E-Mail Adresse bestätigen und sich anmelden.

Im Git Client erstellen wir einen Ordner in welchem wir das Repository Herunterladen können.

SSH-Key erstellen und hinzufügen
--
Im Git-Bash folgenden Befehl eingeben: _$ ssh-keygen -t rsa -b 4096 -C 'DEINE EMAILADRESSE'_ Nun wird ein SSH-Key generiert, diesen Kopieren. Jetzt wechseln Sie zurück auf Ihren github Account.
* Unter Benutzerkonto Settings aufrufen
* Nun auf den Abschnitt SSH und GPG keys wechseln
* New SSH-Key wählen
* Hier den Kopierten SSH-Key hineinkopieren und speichern

Git Client
--
Zuerst den Installer Herunterladen: _https://git-scm.com/downloads_ Ein GUY leitet Sie ganz einfach durch alles Notwendige.

Nun in den Git Bash wechseln und im gewünschten Ordner folgenden Befehl eingeben:_$ git clone https://github.com/mc-b/M300_ (Der Link muss natürlich Ihrem Pfad entsprechen)

Um weitere Schritte durchzuführen, können Sie dieses Glossar verwenden:

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

Kurzer Test:

![vagrant](file:///C:/Users/laura/Documents/vagrant.PNG)



Atom (Visual Studio Code)
--

Nun sollten wir einen Editor Herunterladen. Ich habe mich für Atom entschieden, da ich diesen schon kannte und besser damit klarkomme.

Unter: _https://atom.io/_ lässt sich die neuste Version Downloaden.

#### Extentions Installieren

Wir fügen dem Editor folgende Extentions hinzu:

* Markdown All in One
* Vagrant Extension
* vscode-pdf Extension

Jedoch können wir dies bei Atom auslassen, da bei diesem Editor schon alles integriert ist.
