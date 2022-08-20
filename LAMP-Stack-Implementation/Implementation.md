# _LAMP STACK IMPLEMENTATION_ :penguin: :feather: :dolphin: :elephant:
LAMP stack is a collection of technologies which allows the creation and delivery of web applications or websites. The LAMP stack consists of Linux, Apache, MYSQL and PHP, all these tools are free and Open-Source tools. I will be implementing this LAMP stack using an AWS EC2 instance of Ubuntu Linux

### STEP 1: Create an EC2 instance on AWS
- Login to AWS and launch an instance using EC2

_**See Screenshot below**_
![launch EC2 instance](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/launch%20instance.png)


- Select Instance type of Ubuntu and launch instance.

_**See Screenshot below**_
![Instance Type(Ubuntu)](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/instance%20type.png)


- Once instance has successfully been created, connect to instance.

#### _Instance successfully created and connected to. :heavy_check_mark:_

### STEP 2: Update OS and install Apache Web Server
- Run:
```
sudo apt update
```
- to update system

_**See Screenshot below**_
![update system](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/update%20system.png)


- Apache is a Web Server which is what actually hosts our web application or website
- Install Apache Web Server:
```
sudo apt install apache2
```

_**See Screenshot below**_
![install Apache](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20apache2.png)


- Start Apache and ensure Apache is running:
```
sudo systemctl start apache2
```
```
sudo systemctl status apache2
```

_**See Screenshot below**_
![start and check Apache status](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20apache2.png)


- Copy Public IP of instance and paste it as url to internet browser to check if Apache is really working.
- Output should be as follows:

_**See Screenshot below**_
![Apache is working!](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/check%20apache%20on%20web%20browser.png)


#### _Apache successfully installed :heavy_check_mark:_


### STEP 3: Install MYSQL
- MYSQL is a database for our web application or website
- Install MYSQL
```
sudo apt install mysql-server
```

_**See Screenshot below**_
![mysql server](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20mysql-server.png)


- Use _mysql_secure_installation_ script to secure mysql server, this comes installed with MYSQL
```
sudo mysql_secure_installation
```

_**See Screenshot below**_
![mysql script run](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20secure%20install%20attempt.png)

### :triangular_flag_on_post: COMMON ERROR
- :triangular_flag_on_post: Sometimes when running this script, an error is thrown when trying to create root password.

_**See Screenshot below**_
![mysql script error](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20secure%20error.png)

- :triangular_flag_on_post: To solve this issue login to mysql using ```sudo mysql``` and query:
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'EnterSecurePassword'
```

_**See Screenshot below**_
![resolve mysql secure error](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20reslove%20error.png)


- :triangular_flag_on_post: run ```exit``` query to exit mysql. mysql_secure_installation script should be working without error now.

_**See Screenshot below**_
![mysql script works successfully](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/proof%20error%20has%20been%20resolved.png)


- Login to mysql using the password created and then exit mysql
```
sudo mysql -u root -p
```

_**See Screenshot Below**_
![access mysql and exit](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/log%20in%20and%20exit%20mysql.png)

#### _MYSQL successfully installed :heavy_check_mark:_

### STEP 4: Install PHP
- PHP is a scripting language as well as a runtime which will process code to display content to the end user
- The server will need a module php-mysql which allows PHP communication with mysql database
- libapache2-mod-php package is needed to allow Apache to handle PHP files
- To install these packages run:
```
sudo apt install php libapache2-mod-php php-mysql
```

_**See Screenshot Below**_
![install php](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20php.png)

### Stack successfully implemented :heavy_check_mark:

### STEP 5: Test Setup
- To test setup with PHP script setup a virtual host to hold the website files
- Goal is to setup a domain called _testProject_
- add directory ```/var/www/testProject``` where website will serve documents from.
```
sudo mkdir /var/www/testProject
```
- Then create file _index.php_ in the directory
```
sudo nano /var/www/testProject/index.php
```

_**See Screenshot Below**_
![create testProject dir. and index.php](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/create%20test%20dir%20and%20index.php.png)


- In the _index.php_ file enter the following code:
```
<?php
phpinfo();
```
- create a virtual hosts configuration file in the _/etc/apache2/sites-available_ directory
- copy the default configuration file which comes installed Apache and edit it to use for the _testProject_ website
```
cd /etc/apache2/sites-available/
```
```
sudo cp 000-default.conf testProject.conf
```

_**See Screenshot Below**_
![create testProject config file](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/create%20test%20conf%20file.png)


- In the _testProject.conf_ do the following:
![configurate testProject.conf](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/file%20configuration.png)

- Enable the _testProject_ site:
```
sudo a2ensite testProject.conf
```
- Disable the default site:
```
sudo a2dissite 000-default.conf
```
- Reload Apache daemon to ensure all configurations are implemented
```
sudo systemctl reload apache2
```

_**See Screenshot Below**_
![enable site and disable default](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/enable%20test%20disable%20default%20site.png)

- The default DirectoryIndex settings in the file _/etc/apache2/mods-available/dir.conf_ means that files label _.html_ will take priority over files which have the _.php_ extension. Edited this file and change this.
```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```
- Reload apache to ensure the changes take effect.
```
sudo systemctl reload apache2
```
- Ensure that Apache is running
```
sudo systemctl status apache2
```


_**See Screenshot Below**_
![check status apache(again)](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/check%20apache2%20status.png)

- Copy instance public IP and paste into web browser as url to view virtual hosted website.
- Output is as follows:

_**See Screenshot Below**_
![testProject website is active](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/proof%20test%20is%20running.png)

## SUCCESS :1st_place_medal:
