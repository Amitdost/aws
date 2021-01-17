CREATE INSTANCE Go to EC2 Launch Instance

From Amazon Machine Image choose “ (Ubuntu Server 16.04), LTS HVM SSD Volume Type 64 bit”

From Choose Instance Type select t2.micro In Configure Instance “Enable termination protection” Nothing to do in Add Storage Add Tags (appideasschoolerp : appideasschoolerp it is for this project) Name a security group and Add a rule for HTTP Create and download a key pair Launch

install awscli first 2. INSTALL APACHE, MYSQL and PHPMYADMIN

First connect to SSH sudo -i key username@publicurl

sudo apt-get update sudo apt-get install apache2 libapache2-mod-php7.0 mysql-server php7.0-mysql php7.0 Passsword : appideasschoolerp3785$$THjy! (mysql password, user : root) C. sudo service apache2 restart D. mysql_secure_installation Select no for validate password Select no for change password Select yes to remove anonymous user Select no for login remotely Select yes to remove test database Select yes to reload table privileges E. mysql -u root -p (can connect to mysql console - current not required)

sudo apt-get install phpmyadmin Select apache2 For db config-common Select No sudo service apache2 restart go to /var/www/html (if required that phpmyadmin not in html folder) sudo ln -s /usr/share/phpmyadmin /var/www/html (if required that phpmyadmin not in html folder)

Increase the upload size of phpmyadmin

Cd etc/php/7.0/apache2 Sudo nano php.ini

To enable mod rewrite

sudo a2enmod rewrite sudo service apache2 restart

To enable cors header

sudo a2enmod headers sudo service apache2 reload

To set up mail sudo apt-get install postfix

=======================================================================================================================================================

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
