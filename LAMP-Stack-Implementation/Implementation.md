# _LAMP STACK IMPLEMENTATION_ :penguin: :feather: :dolphin: :elephant:
LAMP stack is a collection of technologies which allows the creation and delivery of web applications or websites. The LAMP stack consists of Linux, Apache, MYSQL and PHP, all these tools are free and Open-Source tools. I will be implementing this LAMP stack using an AWS EC2 instance of Ubuntu Linux

### STEP 1: Create an EC2 instance on AWS
- Login to AWS and launch an instance using EC2

_**Screenshot below**_
![launch EC2 instance](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/launch%20instance.png)


- Select Instance type of Ubuntu and launch instance.

_**Screenshot below**_
![Instance Type(Ubuntu)](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/instance%20type.png)


- Once instance has successfully been created, connect to instance.

#### _Instance successfully created and connected to. :heavy_check_mark:_

### STEP 2: Update OS and install Apache Web Server
- Run:
```
sudo apt update
```
- to update system

_**Screenshot below**_
![update system](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/update%20system.png)


- Install Apache Web Server:
```
sudo apt install apache2
```

_**Screenshot below**_
![install Apache](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20apache2.png)


- Start Apache and ensure Apache is running:
```
sudo systemctl start apache2
```
```
sudo systemctl status apache2
```

_**Screenshot below**_
![start and check Apache status](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20apache2.png)


- Copy Public IP of instance and paste it as url to internet browser to check if Apache is really working.
- Output should be as follows:

_**Screenshot below**_
![Apache is working!](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/check%20apache%20on%20web%20browser.png)


#### _Apache successfully installed :heavy_check_mark:_


### STEP 3: Install MYSQL
- Install MYSQL
```
sudo apt install mysql-server
```

_**Screenshot below**_
![mysql server](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/install%20mysql-server.png)


- Use _mysql_secure_installation_ script to secure mysql server, this comes installed with MYSQL
```
sudo mysql_secure_installation
```

_**Screenshot below**_
![mysql script run](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20secure%20install%20attempt.png)

### :triangular_flag_on_post: COMMON ERROR
- :triangular_flag_on_post: Sometimes when running this script, an error is thrown when trying to create root password.

_**Screenshot below**_
![mysql script error](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20secure%20error.png)

- :triangular_flag_on_post: To solve this issue login to mysql using ```sudo mysql``` and query:
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'EnterSecurePassword'
```

_**Screenshot below**_
![resolve mysql secure error](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/mysql%20reslove%20error.png)


- :triangular_flag_on_post: run ```exit``` query to exit mysql. mysql_secure_installation script should be working without error now.

_**Screenshot below**_
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
