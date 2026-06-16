step 1: create EC2 instance with sg allow http, https, ssh

step 2: connect instance

    sudo apt update && sudo apt upgrade -y
    sudo apt install apache2 -y
    sudo systemctl enable apache2
    sudo systemctl start apache2

step 3: copy the public IP of your EC2 instance and paste it in your browser

    http://ip

step 4: install php

    sudo apt install php libapache2-mod-php -y
    sudo apt install php-mysql -y
    sudo systemctl start mysql

step 6: download latest WordPress files from their official website
    
    wget https://wordpress.org/latest.tar.gz

step 7: Create RDS instance for wordpress
go to ec2 console
create database ->
standard create ->
Mysql ->
give indentity name ->
give user name (admin) ->
self managed ->
vpc (default) ->
give database_name ->


