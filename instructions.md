step 1: create EC2 instance with sg allow http, https, ssh

step 2: connect instance

    sudo apt update && sudo apt upgrade -y
    sudo apt install apache2 -y
    sudo systemctl enable apache2
    sudo systemctl start apache2

step 3: copy the public IP of your EC2 instance and paste it in your browser

    http://ip #if accessed

step 4: install php

    sudo apt install php libapache2-mod-php -y
    sudo apt install php-mysql -y
    php -m | grep mysqli #check

step 5: install mysqlclient

    sudo apt install mysql-client -y

step 6: download latest WordPress files from their official website
    
    wget https://wordpress.org/latest.tar.gz

step 7: Create RDS instance for wordpress
go to ec2 console ->
create database ->
standard create (full configuration) ->
Mysql ->
give indentity name ->
give user name (admin) ->
self managed ->
vpc (default) ->
security group ->
give database_name -> create

step 7: Connect RDS and EC2 instance 

    goto connectivity and security ->
    setup EC2 connection -> connect with your EC2 

step 8: verify the connection to database (again)

    mysql -h <RDS-endpoint> -u admin -p <enter password>
    mysql -h wp-data.ct4wkse4iz17.ap-south-1.rds.amazonaws.com -u admin -p 

check available database 

     show databases; 

first create new database with name for wordpress

     CREATE DATABASE wpdb;

step 9: WordPress Installation 

goto where <wget https://wordpress.org/latest.tar.gz> fetched

    ls
    tar -xzf latest.tar.gz
    ls
    sudo cp -r wordpress/* /var/www/html/


    sudo usermod -a -G apache2 ubuntu
    sudo chown -R ubuntu:apache2 /var/www

step 10: create a copy of wp-config-sample.php file and name it wp-config.php

    cd /var/www/html
    ls
    cp wp-config-sample.php wp-config.php


enter your database name/ username / password / RDS Endpoint

    nano wp-config.php 

![change config](wpconfig.png)

    sudo vim /etc/apache2/apache2.conf


debug: `ls /var/www/html/` if index.html page lists
 
    sudo rm /var/www/html/index.html
    
![change None to All](apache.png)

    sudo systemctl restart apache2 
    
# check on browser that wordpress page show?
if not
debug: give permissions

    sudo chown -R www-data:www-data /var/www/html
    sudo find /var/www/html -type d -exec chmod 755 {} \;
    sudo find /var/www/html -type f -exec chmod 644 {} \;
    sudo systemctl restart apache2
 
step 11: check again on browser 
    
    wordpress shows

step 12:

    give sample site name
    username -> save password -> install wordpress
login

    username
    password
    now you can run webpages
