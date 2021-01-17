To create a sub-domain in follow the steps:

Connect to the ftp Go to var/www Create a folder name vhosts Create a folder for the url you want such as subdomain.example.com Connect to the ssh via terminal

Check url for ssh install in system -http://ubuntuhandbook.org/index.php/2014/09/enable-ssh-in-ubuntu-14-10-server-desktop/

ssh -i mykey.pem user@mydomain.com -Mykey.pem with there full directory path -User in used in ftp -Mydomain.com will be ip or domain name

Do cd .. two times Go to etc/apache2/sites-available sudo nano subdomain.example.com.conf Write the following code in the file

<VirtualHost *:80>

ServerAdmin webmaster@localhost ServerName subdomain.example.com ServerAlias subdomain.example.com DocumentRoot /var/www/vhosts/subdomain.example.com <Directory /var/www/vhosts/subdomain.example.com> Order allow,deny allow from all </Directory> ErrorLog ${APACHE_LOG_DIR}/error.log CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

Save the file

sudo a2ensite subdomain.example.com.conf

To disable it: sudo a2dissite 000-default.conf

To take in effect when disable or enable it is required to restart the server.

Increase the upload size of phpmyadmin

Cd etc/php/7.0/apache2 Sudo nano php.ini

To enable mod rewrite

sudo a2enmod rewrite sudo service apache2 restart

To enable cors header

sudo a2enmod headers sudo service apache2 reload

To set up mail sudo apt-get install postfix

To enable curl sudo apt-get install php7.0-curl sudo netstat -nupt -l (list of listening ports)

sudo ufw allow 443/tcp (allow the port)

sudo lsof -iTCP -sTCP:LISTEN -P (list the services that are running)

sudo a2enmod ssl sudo a2ensite default-ssl sudo /etc/init.d/apache2 restart
