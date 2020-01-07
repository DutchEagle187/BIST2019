M300 - LB1 - Fabian Scherer & Loris Cicilano
======

## Kennt die Vagrant-Befehle

https://user-images.githubusercontent.com/47855918/54756122-d84d8b80-4be7-11e9-8d4b-ee62e54122f7.jpg


## Eingerichtete Umgebung
Webserver mit MySQL & UserInterface [Adminer](https://www.adminer.org/)

## Lokal Firewall installiert & Regel für SSH Zugang gesetzt
Eine lokale Firewall wird installiert und anschliessend auch konfiguriert. Dabei öffnen man den Port 22 um via SSH darauf zuzugreifen. INFO-INPUT SSH Port 22 | TELNET Port 23
```
#Local Firewall installieren
sudo apt-get -y install ufw gufw 
sudo ufw allow from 10.0.2.2 to any port 22
sudo ufw --force enable    
```
## Reverse-Proxy eingerichtet

Im folgenden Schritt wird der Reverse-Proxy eingerichtet:

	sudo ufw allow from 10.0.2.2 to any port 22
	sudo ufw allow 80/tcp
    	sudo ufw --force enable
    	sudo apt-get install libapache2-mod-proxy-html -y
    	sudo apt-get install libxml2-dev -y
    	a2enmod proxy
    	a2enmod proxy_html
    	a2enmod proxy_http
    	sed -i '$aServerName localhost' /etc/apache2/apache2.conf
    	service apache2 restart
    	cd 	/etc/apache2/sites-enabled
    	wget https://pastebin.com/raw/GbjFC2ii
    	cp GbjFC2ii 001-reverseproxy.conf

## Funktionsweise Testen

Um zum überprüfen ob der Webserver läuft wird: http://localhost:8080/ im Browser eingegeben und dann sollte die Startseite angezeigt werden.
Um auf das Adminer UserInterface zu kommen, kann entweder der Direktlink http://localhost:8080/adminer.php oder der Spielplan aufgerufen werden.

## Adminer Interface
Login: root
PW: admin

## Vergleich Vorwissen - Wissenszuwachs
Ich habe gelernt wie man mit einem VagrantFile eine VM erstellt nach seinen Bedürfnissen. Ausserdem habe ich mir sehr viel Fachwissen bezüglich Git, Markdown , Linux und Virtualisierung angeeignet. Zuerst war es für mich sehr schwierig aber mit der Zeit ging es dann. Vor dem Modul wusste ich eigentlich nichts, da wir aber mehrheitlich Linux Server in der Firma haben, konnte ich viel von den Mitarbeitern profitieren. Ich verstehe nun schon sehr viel von der Virtualisierung und weiss wie man z.B. schnell einen Webserver mit MYSQL aufziehen kann. 

## Reflexion
Ich hatte noch nie etwas von Vagrant gehört. Deswegen hatte ich am Anfang noch viel Mühe. Eine VM zu erstellen mit einem Text-File nach seinen Bedürfnissen? Das ist sehr praktisch und zeitsparend. Ich werde in Zukunft sicher mehr mit Vagrant arbeiten und Zuhause Test-Umgebungen aufzuziehen, da so IT Skills praktisch direkt anwendbar sind. 