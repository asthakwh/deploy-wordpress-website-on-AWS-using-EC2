# WordPress Deployment on AWS EC2 with RDS

## Project Overview

This project demonstrates how to deploy a **WordPress website** on an **AWS EC2 Ubuntu instance** using **Apache and PHP**, while storing website data in an **Amazon RDS MySQL database**.

The objective is to separate the application server and the database server, following a scalable cloud architecture.

---

## Architecture

```
                +----------------------+
                |      Web Browser     |
                +----------+-----------+
                           |
                           |
                    HTTP (Port 80)
                           |
                           v
                +----------------------+
                |   AWS EC2 (Ubuntu)   |
                | Apache + PHP         |
                | WordPress            |
                +----------+-----------+
                           |
                    MySQL (Port 3306)
                           |
                           v
                +----------------------+
                |   Amazon RDS MySQL   |
                | WordPress Database   |
                +----------------------+
```

---

## Technologies Used

* AWS EC2 (Ubuntu)
* Amazon RDS (MySQL)
* Apache2
* PHP
* MySQL Client
* WordPress

---

## Prerequisites

* AWS Account
* EC2 Instance
* RDS MySQL Instance
* Security Group allowing:

  * SSH (22)
  * HTTP (80)
  * HTTPS (443)
  * MySQL (3306) from EC2 to RDS

---

## Deployment Steps

### 1. Launch EC2 Instance

* Create Ubuntu EC2 instance.
* Configure Security Group to allow:

  * SSH
  * HTTP
  * HTTPS

### 2. Install Apache

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
```

Verify:

```
http://<EC2-Public-IP>
```

---

### 3. Install PHP

```bash
sudo apt install php libapache2-mod-php -y
sudo apt install php-mysql -y
```

Verify:

```bash
php -m | grep mysqli
```

---

### 4. Install MySQL Client

```bash
sudo apt install mysql-client -y
```

---

### 5. Download WordPress

```bash
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
```

---

### 6. Create Amazon RDS

* Create MySQL database
* Configure credentials
* Create database instance
* Connect EC2 with RDS using the Connectivity & Security settings

---

### 7. Verify Database Connection

```bash
mysql -h <RDS-ENDPOINT> -u admin -p
```

Create a database for WordPress:

```sql
CREATE DATABASE wpdb;
```

---

### 8. Copy WordPress Files

```bash
sudo cp -r wordpress/* /var/www/html/
```

Remove Apache default page if present:

```bash
sudo rm /var/www/html/index.html
```

---

### 9. Configure WordPress

```bash
cd /var/www/html
cp wp-config-sample.php wp-config.php
nano wp-config.php
```

Update:

* DB_NAME
* DB_USER
* DB_PASSWORD
* DB_HOST

---

### 10. Configure Apache

Edit:

```
/etc/apache2/apache2.conf
```

Change:

```
AllowOverride None
```

to

```
AllowOverride All
```

Restart Apache:

```bash
sudo systemctl restart apache2
```

---

### 11. Set Permissions

```bash
sudo chown -R www-data:www-data /var/www/html
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;
sudo systemctl restart apache2
```

---

### 12. Complete WordPress Setup

Open:

```
http://<EC2-Public-IP>
```

Provide:

* Site Title
* Username
* Password
* Email

Click **Install WordPress**.

---

## Verification

* Apache service running successfully
* EC2 successfully connected to RDS
* WordPress installation page displayed
* Website accessible through EC2 Public IP
* Admin login working successfully

---

## Outcomes

* Deploying applications on AWS EC2
* Configuring Apache and PHP
* Connecting EC2 with Amazon RDS
* Configuring WordPress manually
* Managing Linux permissions and services
* Troubleshooting web server deployment issues

---

