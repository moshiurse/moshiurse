#### Installing Nginx

Follow this Link 
https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04

> sudo apt update <br>
> sudo apt install nginx<br>
> sudo ufw app list<br>
> sudo ufw allow 'Nginx HTTP'<br>
> sudo ufw status<br>

if it is showing **inactive** that means your firewall is disabled 
Run this command 
> sudo ufw enable

Now check nginx status
> sudo systemctl status nginx

It must show running. Now test the process.

You can access the default Nginx landing page to confirm that the software is running properly by 
navigating to your server’sIP address. If you do not know your server’s IP address,
you can get it a few different ways.

``` 
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//' 
```

##### Managing nginx process
> sudo systemctl stop nginx // **start stop restart reload disable enable** (default nginx is enabled)

If you are simply making configuration changes, you can often reload Nginx without dropping
connections instead of restarting it. To do this, type the following:

> sudo systemctl reload nginx

#### Install Nodejs

Follow this link
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04

Personally I recommend install node with nvm.

#### Install PHP
Follow this Link
(https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Nginx-PHP-FPM-config-example)

sudo apt-get update -y

sudo apt-get upgrade -y

sudo apt-get install php8.1-fpm -y
sudo systemctl status php8.1-fpm
sudo nano /etc/nginx/sites-available/default

Changes Portion 
# Add index.php to setup Nginx, PHP & PHP-FPM config
  index index.php index.html index.htm index.nginx-debian.html;
  
    # pass PHP scripts on Nginx to FastCGI (PHP-FPM) server
  location ~ \.php$ {
    include snippets/fastcgi-php.conf;

    # Nginx php-fpm sock config:
    fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    # Nginx php-cgi config :
    # Nginx PHP fastcgi_pass 127.0.0.1:9000;
  }
  
  #### if Apache and Nginx document roots concur
  location ~ /\.ht {
    deny all;
  }

sudo nginx -t
sudo systemctl restart nginx
sudo chmod -R 777 /var/www/html
echo "<?php phpinfo(); ?>" >> /var/www/html/info.php

Install some additional php extension

apt install openssl php-bcmath php-curl php-json php-mbstring php-mysql php-tokenizer php-xml php-zip

#### Install mariadb server or mysql server

https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04
https://www.digitalocean.com/community/tutorials/how-to-install-mariadb-on-ubuntu-20-04

To create users and permission for database 

https://www.hostinger.com/tutorials/mysql/how-create-mysql-user-and-grant-permissions-command-line

A nice tiutorial on Install Linux, Nginx, MySQL, PHP (LEMP stack) on Ubuntu
https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-20-04

#### Install composer 
https://getcomposer.org/download/

#### Install git
normally git is installed by default
https://www.atlassian.com/git/tutorials/install-git


#### Secure HTTPS with Certbot/Lets encrypt
https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04

