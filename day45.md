---
title: "Deploy Wordpress Website on AWS"
datePublished: Mon Dec 11 2023 19:24:54 GMT+0000 (Coordinated Universal Time)
cuid: clq1az9r2000108l37uqf7u7b
slug: deploy-wordpress-website-on-aws
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1702322531754/16f9445a-3221-4a98-bd8e-3deef85a6592.png
tags: devops, iw, 90daysofdevops

---

Over 30% of all websites on the internet use WordPress as their content management system (CMS). It is most often used to run blogs, but it can also be used to run e-commerce sites, message boards, and many other popular things. This guide will show you how to set up a WordPress blog site.

## Task-01

* As WordPress requires a MySQL database to store its data, create an RDS as you did on Day 44
    

To configure this WordPress site, you will create the following resources in AWS:

* An Amazon EC2 instance to install and host the WordPress application.
    
* An Amazon RDS for MySQL database to store your WordPress data.
    
* Set up the server and post your new WordPress app.
    

**Step 1: Create an RDS Database:** Create an RDS Database just like we created on Day 44: [RDS set-up day 44](https://hashnode.com/post/clpyf21s0000608joe648dkxw)

**Step 2: Create an EC2 Instance**

**Step 3: Configure your Amazon RDS Database**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702312625154/446b331a-8e99-4ef5-be3a-e9f95dae7d31.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702312656066/de971e32-cf7e-406c-88ab-0554f753a28a.png align="center")

Edit the **inbound rules** to change the rules for your security group. Change the **Type** property to **MYSQL/Aurora**, which will update the **Protocol** and **Port range** to the proper values. Then, remove the current security group value configured for the **Source**. Choose the **wordpress** security group that you used for your EC2 instance.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702313309282/f8ef0dee-f597-41e5-aaf5-c5e78e7a6185.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702313133012/05f562a0-1e0e-4bda-97cd-e8b09535e28d.png align="center")

Connect to EC2 instance using SSH

Run the following command in your terminal to install a MySQL client:

```plaintext
sudo apt update -y && sudo apt install mysql-client -y
```

Login to the database server using the below command:

```plaintext
mysql -h <endpoint> -P 3306 -u admin -p
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702314038573/fd36b845-f4e6-4a99-95c5-bedbcdcb63ca.png align="center")

Create a database and user with the following command:

```bash
CREATE DATABASE wordpress;
CREATE USER 'wordpress' IDENTIFIED BY 'wordpress-pass';
GRANT ALL PRIVILEGES ON wordpress.* TO wordpress;
FLUSH PRIVILEGES;
Exit
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702314469693/7117ad1f-d227-4f5f-b0b2-a6daa33cfd66.png align="center")

We need to install Apache on our instance to run a web server

```bash
sudo apt-get install apache2 -y
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702315291608/91816843-d959-4cfc-b192-1da7ff906d7a.png align="center")

Go to your instance, click on it copy the **Public IPv4** address and open it in your web browser.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702315462423/af1f1cc4-6d3b-474d-a7bb-9e8579c210ad.png align="center")

Download and configure wordpress on the instance

```bash
 wget https://wordpress.org/latest.tar.gz 
 tar -xzf latest.tar.gz
# you can run ls to view the contents of the directory
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702316513677/99fb36ba-b7ce-43b6-af96-fabf05b728d3.png align="center")

Change the directory to the WordPress directory and make a copy of the `cp wp-config-sample.php` with the below command:

```bash
cd wordpress
cp wp-config-sample.php wp-config.php
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702319192931/291c5ce8-be2f-4f54-a45b-b955def82373.png align="center")

```apache
DB_NAME: “wordpress”
DB_USER: The name of the user you created in the database 
DB_PASSWORD: The password for the user you created for the database
DB_HOST: The hostname of the database that you created 
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702319295757/735b3cff-0128-4fd4-809f-9624c3f71083.png align="center")

```apache
define( 'AUTH_KEY',         'put your unique phrase here' );
define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
define( 'NONCE_KEY',        'put your unique phrase here' );
define( 'AUTH_SALT',        'put your unique phrase here' );
define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
define( 'NONCE_SALT',       'put your unique phrase here' );
```

The values for this configuration can be found [here](https://api.wordpress.org/secret-key/1.1/salt/)

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702319369711/78ca6f9a-913c-4919-b0c3-60e3604b9e9b.png align="center")

Now, we will install the application dependencies we need for WordPress

```apache
sudo apt install php libapache2-mod-php php-mysql -y
```

Then, we will **copy** the file contents from the **WordPress folder** to the **/var/www/html** folder to configure the application with the Apache web server.

```apache
sudo cp -r wordpress/* /var/www/html/
```

Restart the Apache web server.

```apache
sudo systemctl restart apache2
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702320474454/385da472-f81f-43cd-ba82-6ffb60c4aee3.png align="center")

Then, we will navigate to the **public-IP/wp-admin/**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1702321319601/48080ee2-8c25-4253-bb34-881b210adb64.png align="center")

Thank you.
