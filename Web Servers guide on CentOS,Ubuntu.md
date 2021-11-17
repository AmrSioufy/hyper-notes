# Welcome to the Web Servers guide! #
#### _Note1 : The below content was written while studying/doing labs on it._ ####
#### _Note2 : This is a beginners guide, the below steps can be done in a several advanced ways_ ####

## CentOS 7 ##
_We will install LAMP, configure virtual host, install wordpress, secure using SSL._
### LAMP stack ###
##### _LAMP means Linux/Apache/MySQL/php_ #####

To make the stack work we will do the following steps

- `sudo yum install httpd` # installing apache #
- `sudo systemctl start httpd.service` # starting apache #
- `sudo systemctl enable httpd.service` # enabling apache on boot #
- `sudo firewall-cmd --permanent --zone=public --add-service=http` # allowing http port in firewall #
- `sudo firewall-cmd --permanent --zone=public --add-service=https` # allowing https port in firewall #
- `sudo firewall-cmd --reload` # reloading firewall for changes to take effect #
- `sudo yum install mariadb-server mariadb` # installing mariadb #
- `sudo systemctl start mariadb` # starting mariadb #
- `sudo mysql_secure_installation` # installing mysql #
- `sudo systemctl enable mariadb.service` # enabling mariadb on boot #
- `sudo yum install php php-mysql` # installing php #
- `sudo systemctl restart httpd.service` # restarting apache #
- `sudo yum install yum-utils –y` 
- `sudo yum install epel-release –y`
- `sudo yum install http://rpms.remirepo.net/enterprise/remi-release-7.rpm`
- `sudo yum-config-manager ––enable remi–php74` # enabling php version 7.4 #
- `sudo yum install php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql –y` # installing other php versions #

### Creating a virtual host ###
- `sudo mkdir -p /var/www/example.com` # making a directory for our virtual host #
- `sudo nano /etc/httpd/conf.d/example.com.conf` # creating a configuration file for the vh and applying the below template #

```
<VirtualHost *:80>
    ServerName example.com
    ServerAlias www.example.com
    ServerAdmin webmaster@example.com
    DocumentRoot /var/www/example.com/

    <Directory /var/www/example.com/>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/example.com-error.log
    CustomLog /var/log/httpd/example.com-access.log combined
</VirtualHost>
```
- `sudo nano /etc/hosts` # update the conf file by adding webserver-ip , virtualhost domain , virtual host conf file path #
- `sudo systemctl restart httpd` 

### SSL Cert ###
##### We want to make sure that the latest epel release is installed so you may update or install
##### We will use certbot as our service 
- `sudo yum install epel-release` 
- `sudo yum install certbot python2-certbot-apache` # installing certbot #
- `sudo certbot --apache -d example.com` # apply cerbot on our virtual host domain #

### Creating Wordpress in mariadb DATABASE ###
- `sudo mysql -u root -p` #connecting to mysql shell using root
- `CREATE DATABASE wordpress;` #creating a database
- `GRANT ALL ON wordpress.* TO 'wordpress'@'localhost' IDENTIFIED BY 'secret';` #giving a password to the database   
- `FLUSH PRIVILEGES;`#updating privileges
- `quit`

### Installing Wordpress ###
- `cd /var/www/example.com`#Navigating to our virtualhost document root
- `sudo wget https://wordpress.org/latest.tar.gz`#Pulling/extracting/installing wordpress
- `sudo tar xvzf latest.tar.gz` 
- `sudo rm -v latest.tar.gz` 
- `sudo chown -Rf apache:apache ./wordpress/` #Applying user and group "apache" to the file wordpress 
- `sudo chmod -Rf 775 ./wordpress/`#Giving rwx to wordpress 
- `sudo systemctl restart httpd` 

## CentOS 8 ##

### LAMP ###
Note: Comments on commands are the same as ones done in CentOS 7

- `sudo dnf install httpd httpd-tools`
- `sudo systemctl enable httpd`
- `sudo systemctl start httpd`
- `sudo firewall-cmd --permanent --zone=public --add-service=http`
- `sudo firewall-cmd --permanent --zone=public --add-service=https`
- `sudo firewall-cmd --reload`
- `sudo dnf install mariadb-server mariadb -y`
- `sudo systemctl start mariadb`
- `sudo systemctl enable mariadb`
- `sudo mysql_secure_installation`
- `sudo dnf install https://dl.fedoraproject.org/pub/epel/epel-release-l`
- `sudo dnf install install dnf-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`
- `sudo dnf module reset php`
- `sudo dnf module enable php:remi-7.4`
- `sudo dnf install php php-opcache php-gd php-curl php-mysqlnd`

### Creating VirtualHost ###
- `sudo mkdir -p /var/www/example.com`
- `sudo nano /etc/httpd/conf.d/example.com.conf`

```
<VirtualHost *:80>
    ServerName example.com
    ServerAlias www.example.com
    ServerAdmin webmaster@example.com
    DocumentRoot /var/www/example.com/

    <Directory /var/www/example.com/>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>

    ErrorLog /var/log/httpd/example.com-error.log
    CustomLog /var/log/httpd/example.com-access.log combined
</VirtualHost>

```
- `sudo systemctl restart httpd`

### SSL Cert ###
- `sudo dnf install epel-release`
- `sudo dnf install certbot python3-certbot-apache`
- `sudo certbot --apache -d amr.test.safaamsa.com`

### Creating wordpress in mariadb Database ###
- `sudo mysql -u root -p`
- `CREATE DATABASE wordpress;`
- `GRANT ALL ON wordpress.* TO 'wordpress'@'localhost' IDENTIFIED BY 'secret';`
- `FLUSH PRIVILEGES;`
- `quit`
### Installing Wordpress ###
- `cd /var/www/example.com`
- `sudo wget https://wordpress.org/latest.tar.gz`
- `sudo tar xvzf latest.tar.gz`
- `sudo rm -v latest.tar.gz`
- `sudo chown -Rf apache:apache ./wordpress/`
- `sudo chmod -Rf 775 ./wordpress/`
- `sudo systemctl restart httpd`


## Ubuntu ##
- `sudo sed -i /cosmic/bionoc ------ ` # Changing Ubuntu version from cosmic to bionic

### LAMP ###
- `sudo apt update`
- `sudo apt upgrade`
- `sudo apt install -y apache2 apache2-utils`
- `sudo systemctl start apache2`
- `sudo systemctl enable apache2`
- `sudo apt install mariadb-server mariadb-client`
- `sudo systemctl start mariadb`
- `sudo systemctl enable mariadb`
- `sudo mysql_secure_installation`
- `sudo apt install php libapache2-mod-php`
- `sudo a2enmod php7.2`
- `sudo systemctl restart apache2`


### Creating a virtual host ###
- `sudo mkdir -p /var/www/example.com`
- `sudo chmod -R 755 /var/www`
- `sudo nano /etc/apache2/sites-available/example.com.conf`

```
<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com/
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

```
- `sudo systemctl reload apache2`
- `sudo a2ensite example.com.conf`
- `sudo a2dissite 000-default.conf`
- `sudo systemctl reload apache2`

### Creating Wordpress in mariadb DATABASE ###
- `sudo mysql -u root -p`
- `CREATE DATABASE wordpress;`
- `GRANT ALL ON wordpress.* TO 'wordpress'@'localhost' IDENTIFIED BY 'secret';`
- `FLUSH PRIVILEGES;`
- `quit`

### Installing Wordpress ###
- `cd /var/www/example.com`
- `sudo wget https://wordpress.org/latest.tar.gz`
- `sudo tar xvzf latest.tar.gz`
- `sudo rm -v latest.tar.gz`
- `sudo chown -Rf www-data:www-data ./wordpress/`
- `sudo chmod -Rf 775 ./wordpress/`
- `sudo systemctl restart apache2`

### Configuring ufw for SSH/HTTPS/SSL for apache then Installing certbot for the SSL certificate ###
- `sudo a2enmod ssl`
- `sudo ufw default deny incoming`
- `sudo ufw default allow outgoing`
- `sudo ufw allow ssh`
- `sudo ufw allow 22`
- `sudo ufw enable`
- `sudo ufw allow 'Apache Full'`
- `sudo ufw delete allow 'Apache'`
- `sudo ufw allow '443/tcp'`
- `sudo ufw allow '443'`
- `sudo add-apt-repository ppa:certbot/certbot`
- `sudo apt install python-certbot-apache`
- `sudo certbot --apache -d amr.test.safaamsa.com`
- `sudo certbot renew --dry-run`
- `sudo apache2ctl configtest` # Checks if virtualhost conf file has syntax error 
