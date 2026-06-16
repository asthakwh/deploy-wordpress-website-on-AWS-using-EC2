step 1: create EC2 instance with sg allow http, https, ssh

step 2: connect instance

    sudo apt update && sudo apt upgrade -y
    sudo yum install -y apache2
    sudo systemctl start apache2
    sudo systemctl enable apache2
    sudo systemctl restart apache2

