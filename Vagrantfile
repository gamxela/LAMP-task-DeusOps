# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.network "forwarded_port", guest: 8001, host: 8081
  config.vm.network "forwarded_port", guest: 8002, host: 8082

  config.vm.synced_folder ".", "/vagrant_data"

  config.vm.provision "shell", inline: <<-SHELL

  	 sudo apt update

 	 sudo apt install -y apache2 libapache2-mod-php

 	 sudo apt install -y gostscript

 	 sudo apt install -y mysql-server

 	 sudo apt install -y php php-bcmath php-curl php-imagick php-intl php-json php-mbstring php-mysql php-xml php-zip php-gd

	 sudo mysql -e "CREATE DATABASE IF NOT EXISTS wordpress;"
	 sudo mysql -e "CREATE USER wordpress@'localhost' identified by 'wordpress';"
	 sudo mysql -e "GRANT ALL ON wordpress.* TO 'wordpress'@'localhost';"

	 sudo mysql -e "CREATE DATABASE IF NOT EXISTS drupal;"
	 sudo mysql -e "CREATE USER drupal@'localhost' identified by 'drupal';"
	 sudo mysql -e "GRANT ALL ON drupal.* TO 'drupal'@'localhost';"

	 sudo tar -xf /vagrant_data/wordpress.tar.gz -C /var/www
	 sudo chown -R root:www-data /var/www/wordpress
	 sudo cp /vagrant_data/001-wordpress.conf /etc/apache2/sites-available/
	 sudo ln -s /etc/apache2/sites-available/001-wordpress.conf /etc/apache2/sites-enabled/001-wordpress.conf
	 sudo cp /vagrant_data/wp-config.php /var/www/wordpress/wp-config.php
	 sudo chmod ago+w /var/www/wordpress/wp-config.php
	 sudo chmod ago+w /var/www/wordpress/wp-config.php

	 sudo tar -xf /vagrant_data/drupal.tar.gz -C /var/www
	 sudo chown -R root:www-data /var/www/drupal-9.3.11
	 sudo cp /vagrant_data/002-drupal.conf /etc/apache2/sites-available/
	 sudo ln -s /etc/apache2/sites-available/002-drupal.conf /etc/apache2/sites-enabled/002-drupal.conf
	 sudo mkdir /var/www/drupal-9.3.11/sites/default/files
	 sudo mkdir /var/www/drupal-9.3.11/sites/default/translations
     sudo chmod ago+w /var/www/drupal-9.3.11/sites/default/files
     sudo cp /vagrant_data/settings.php /var/www/drupal-9.3.11/sites/default/settings.php
     sudo chmod ago+w /var/www/drupal-9.3.11/sites/default/settings.php
	 sudo rm -rf /etc/apache2/sites-available/000-default.conf

	 sudo cp /vagrant_data/ports.conf /etc/apache2/ports.conf

	 sudo service apache2 restart
	 
  SHELL
end
