# Setting Up a LAMP Server With Raspberry Pi

This repo is just a review of the great material done by the [Random Nerd Tutorials](https://randomnerdtutorials.com/raspberry-pi-apache-mysql-php-lamp-server/).

The main purpose here was to list the steps and commands used to set up the Raspberry Pi with a LAMP server (**L**inux, **A**pache, **M**ySQL, **P**HP).

## Steps Using SSH (Secure Shell) Connection.

### Get SSH Acess to Raspberry PI

Open the bash (Linux or MAC OS) or PowerShell for Windows and type:

**commands**

ssh raspberrypi_user@your_raspberrypi_IP

It will ask for the password configured for the Raspberry Pi user during the Raspbian installation.

### Updating and Upgrading

**commands**:  

raspberrypi_user@your_raspberrypi_IP: sudo apt update && sudo apt upgrade -y

### Install Apache2

**commands**: 

raspberrypi_user@your_raspberrypi_IP: sudo apt install apache2 -y

### Check Apache2 Installation

Access the directory using the commands below and check if there is an "index.html" file

**commands**: 

raspberrypi_user@your_raspberrypi_IP: cd /var/www/html

raspberrypi_user@your_raspberrypi_IP: cd /var/www/html $ ls -la

### Verifying the Raspberry Pi IP

**commands**

raspberrypi_user@your_raspberrypi_IP: hostname -I

### Checking if the server is running

Open your browser and type:

**http://<your_raspberrypi_IP>:**

### Install PHP

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo apt install php -y

### Replacing the index.html to an index.php file

1- Go to the directory **/var/www/html/** again.

**commands**

raspberrypi_user@your_raspberrypi_IP: cd /var/www/html/

2- Remove the file index.html

**commands**

raspberrypi_user@your_raspberrypi_IP: cd /var/www/html $ sudo rm index.html

3- Create the index.php file and edit whichever you wish to write:

**commands**

raspberrypi_user@your_raspberrypi_IP: cd /var/www/html $ sudo nano index.php

4- After opening the nano text editor you can type the following just to test the server running with a different index file:

[verbose]<?php 
    
    echo "Hello world!"

?>

5- Save the file by typing **Ctrl + X** and confirm the file name by pressing **Y** and **Enter**.


### Restart Apache2

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo service apache2 restart

1-Repeat the process before by opening the browser and typing **http://<your_raspberrypi_IP>:**

to see if your index.php will be shown.

2- If everything goes nicely, then you can remove the file index.php from the path **/var/www/html/**

**commands**

raspberrypi_user@your_raspberrypi_IP: /var/www/html $ sudo rm index.php

## Install MySQL (MariaDB Server)

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo apt install mariadb-server php-mysql -y

raspberrypi_user@your_raspberrypi_IP: sudo service apache2 restart

## Setting some security parameters

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo mysql_secure_installation

### It will appear the following message:

------------------------------------------------------------------------
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
haven't set the root password yet, you should just press enter here.

Enter current password for root (enter for none):

------------------------------------------------------------------------

Choose a password and press **Enter**. Don't lose it, because you'll need for the next steps and to get access to manage the MySQL databases used in your projects.

1- Type in **Y** to Remove anonymous users

2- Type in **n** to Dissallow root login remotely 
  |
  | -> This works to give root acces from another terminal connected to the Raspberry Pi using SSH.

3- Type in **Y** to Remove test database and access to it 
4- Type in **Y** to Reload privilege tables now

After that the message "Thanks for using MariaDB!" pops up.

## Install phpMyAdmin

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo apt install phpmyadmin -y

The phpMyAdmin installation process requires you choose some options like:

1- Select **Apache2** when prompted and press **Enter**
2- Configuring **phpmyadmin**? **Yes** and press **Enter**
3- Configure database for phpmyadmin with **dbconfig-common**? **Yes** 
4- Type your **password** and press **OK**

5- Enable the PHP MySQLi extension and restart Apache2:

**commands**

raspberrypi_user@your_raspberrypi_IP: sudo phpenmod mysqli

raspberrypi_user@your_raspberrypi_IP: sudo service apache2 restart

6- Move the phpmyadmin directory to **/var/www/html**

raspberrypi_user@your_raspberrypi_IP:/var/www/html $ sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

## Testing the acess on phpMyAdmin

Load you browser and type **http://<you_raspberrypi_IP>/phpmyadmin** and you shoudl see the phpMyAdming login page:

![Alt Text](images/phpMyAdmin_Login_Page.png)

## Other useful setups:

To deal with you web pages, it's worth to change the permissions for the path **/var/www/html/**.
To do so, type the commands below:

**commands** 

raspberrypi_user@your_raspberrypi_IP: ~ $ ls -lh /var/www/

raspberrypi_user@your_raspberrypi_IP: ~ $ sudo chown -R pi:www-data /var/www/html/

raspberrypi_user@your_raspberrypi_IP: ~ $ sudo chmod -R 770 /var/www/html/

raspberrypi_user@your_raspberrypi_IP: ~ $ ls -lh /var/www/


Thanks.