## _LAMP STACK IMPLEMENTATION_ :penguin: :feather: :dolphin: :elephant:
LAMP stack is a collection of technologies which allows the creation and delivery of web applications or websites. The LAMP stack consists of Linux, Apache, MYSQL and PHP, all these tools are free and Open-Source tools. I will be implementing this LAMP stack using an AWS EC2 instance of Ubuntu Linux

### STEP 1: Create an EC2 instance on AWS
- Login to AWS and launch an instance using EC2

_**Screenshot below**_
![launch EC2 instance](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/launch%20instance.png)


- Select Instance type of Ubuntu and launch instance.

_**Screenshot below**_
![Instance Type(Ubuntu)](https://github.com/Lihle80/Technology-Stacks/blob/main/LAMP-Stack-Implementation/Images/instance%20type.png)


- Once instance has successfully been created, connect to instance.

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


### STEP 3: Install 
