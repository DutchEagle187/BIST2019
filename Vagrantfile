#############################################
# Autor:	Fabian Scherer/ Loris Cicilano	#
# Projekt:  TBZ M300 LB1		 			#
#############################################


Vagrant.configure(2) do |config|
	config.vm.define "Webserver" do |config|
	config.vm.box = "ubuntu/xenial64"
	config.vm.network "forwarded_port", guest:80, host:8080	
	config.vm.synced_folder "C:/Temp/Website", "/Website"
	config.vm.provider "virtualbox" do |vb|
		vb.name = "Webserver"
		vb.memory = "1024" 
end
config.vm.provision "shell", inline: <<-SHELL 
#Update/ Upgrade
	sudo apt-get update
	sudo apt-get -y upgrade
#Gruppe MyAdmin erstellen
	sudo groupadd myadmin
#User erstellen
	sudo useradd admin -g myadmin -m -s /bin/bash
#Password festlegen
	sudo chpasswd <<<admin:admin
#Lokal Firewall installieren & Regel für SSH Zugang setzten
        sudo apt-get -y install ufw gufw 
        sudo ufw allow from 10.0.2.2 to any port 22
		sudo ufw allow 80/tcp
        sudo ufw --force enable
#Installation Apache und Debian Tools
	sudo apt-get -y install debconf-utils 
	sudo apt-get -y install apache2 
#Passwort für MySQL	
	sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password password admin'
	sudo debconf-set-selections <<< 'mysql-server mysql-server/root_password_again password admin'
#Installation von Tools & MYSQL	
	sudo apt-get -y install php libapache2-mod-php php-curl php-cli php-mysql php-gd mysql-client mysql-server 
#Admininer SQL UI einrichten
	sudo mkdir /usr/share/adminer
	sudo wget "http://www.adminer.org/latest.php" -O /usr/share/adminer/latest.php
	sudo ln -s /usr/share/adminer/latest.php /usr/share/adminer/adminer.php
	echo "Alias /adminer.php /usr/share/adminer/adminer.php" | sudo tee /etc/apache2/conf-available/adminer.conf	
	sudo a2enconf adminer.conf 
#Reverse-Proxy einrichten
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
#Website im Apache Verzeichniss	ersetzten
	sudo cp -a /Website/html/. /var/www/html/
SHELL
end
end