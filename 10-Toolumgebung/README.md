10-Toolumgebung
==
Inhalt
--
* Git Account
* Git Client
* Virtual Box
* Vagrant
* Atom (Visual Studio Code)
* Infrastruktur Sicherheit
* Lernvortschritt

Git Account
--
Als erstes werden wir uns einen Git Account erstellen und alles Notwendige dazu Konfigurieren. Dieser Account dient uns als Cloud-Speicher für die Dokumentation.
* Ganz einfach unter www.github.com einen Account erstellen.
* Nun die E-Mail Adresse bestätigen und sich anmelden.

Im Git Client erstellen wir einen Ordner in welchem wir das Repository Herunterladen können.

#### SSH-Key erstellen und hinzufügen

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

<img src="https://github.com/lauradubach/M300/blob/main/10-Toolumgebung/vagrant.PNG" width="500" height="350">

Atom (Visual Studio Code)
--

Nun sollten wir einen Editor Herunterladen. Ich habe mich für Atom entschieden, da ich diesen schon kannte und besser damit klarkomme.

Unter: _https://atom.io/_ lässt sich die neuste Version Downloaden.

#### Extentions Installieren

Wir fügen dem Editor folgende Extentions hinzu:

* Markdown All in One
* Vagrant Extension
* vscode-pdf Extension

Jedoch können wir dies bei Atom **auslassen**, da bei diesem Editor schon alles integriert ist.

Infrastruktur Sicherheit
--
Hier wird beschrieben wie man eine virtualisierte Infrastruktur sicherer machen kann.

#### Firewall Rules
Die Firewall stellt sicher, dass kein Netzwerkverkehr unerlaubt an ihr vorbeirauscht. Nur unbedingt notwendige Zugriffe sollten erlaubt werden.

Hier wird eine VM erstellt welche eine Firewall hat:

```Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox" do |vb|
end

config.vm.provision "shell", inline: <<-SHELL
sudo ufw allow 80/tcp
vagrant ssh web
sudo ufw allow from any to any port 22
sudo ufw allow from any to any port 3306
sudo ufw --force enable
SHELL
end
```   

#### Reverse Proxy

Reverse-Proxys werden in der Regel von einer Firewall abgesichert in einem privaten Netzwerk oder einer vorgelagerten DMZ installiert. Dabei stellt der Reverse-Proxy die einzige Verbindung zwischen Internet und privaten Netzwerk dar. Alle Anfragen an die Server im LAN durchlaufen somit dieselbe Kommunikationsschnittstelle, bevor sie an die eigentlichen Zielsysteme weitergeleitet werden.


```Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox" do |vb|
end

config.vm.provision "shell", inline: <<-SHELL
sudo apt-get install apache2 -y
sudo apt-get install libapache2-mod-proxy-html -y
sudo apt-get install libxml2-dev -y
sudo a2enmod proxy
sudo a2enmod proxy_html
sudo a2enmod proxy_http
sudo echo "ServerName localhost" >> /etc/apache2/apache2.conf
sudo service apache2 restart
sudo touch /etc/apache2/sites-enabled/001-reverseproxy.conf
sudo echo "ProxyRequests Off
    <Proxy *>
        Order deny,allow
        Allow from all
    </Proxy>
    ProxyPass /master http://master
    ProxyPassReverse /master http://master" >> /etc/apache2/sites-enabled/001-reverseproxy.conf
SHELL
end
```
#### Benutzer und Rechteverwaltung

Mit diesem Skript wurden test User, test Gruppen und ein test File angelegt.

```Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/xenial64"
  config.vm.provider "virtualbox" do |vb|
end

config.vm.provision "shell", inline: <<-SHELL
sudo useradd Ferzana
sudo useradd Fabio
sudo useradd Yang
sudo groupadd IT
sudo groupadd KV
sudo groupadd HR
sudo usermod -a -G IT Ferzana
sudo usermod -a -G KV Fabio
sudo usermod -a -G HR Yang
sudo touch file1.txt
SHELL
end
```

#### SSH

Lernvortschritt
--
Vor diesem Modul kannte ich so ziemlich nichts von dem was wir angeschaut haben. Ich wusste nicht was Vagrant ist oder Github, ich hatte auch keine Ahnung was ein Markdown sein könnte. Durch diese Aufgaben, konnte ich alles sehr gut kennenlernen und ausprobieren. Ich kann nun eine VM erstellen nur mit einem einzigen Vagrant Befehl, ich kann mit einem Editor Dokumentieren und ganz einfach mit dem Markdown arbeiten, ich kenne viele Git Befehle und kann diese anwenden. Ich nehme sehr viel mit und habe auch sehr viel neues gelernt, was mir in Zukunft sicher helfen kann. 
