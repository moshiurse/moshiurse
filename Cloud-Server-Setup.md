# Cloud Server setup
## Create a new User with sudo enabled<br>
Sometimes with a root user, things might not work properly. So creating a new user with sudo permission is a better option.

**Login to your server first.**
```
ssh root@your_ip
```
**Add user**(add **sudo** if you see : 'adduser: Only root may add a user or group to the system.')
```
sudo adduser moshiur
```
You will be prompted to create and verify a password for the user. set password twice.<br>
You’ll be asked to fill in some information about the new user. It is fine to accept the defaults and leave this information blank.

**Adding the User to the sudo Group**

```
sudo usermod -aG sudo moshiur
```

**Testing sudo Access**

```
su - moshiur
```

As the new user, verify that you can use sudo by prepending sudo to the command that you want to run with superuser privileges.<br>
For example, you can list the contents of the /root directory, which is normally only accessible to the root user.
```
sudo ls -la /root
```

[You can follow this Link to know elaboratly](https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-22-04-quickstart)

## Installing Nginx

```
sudo apt update
```
```
sudo apt install nginx -y
```
```
sudo ufw app list
```
```
sudo ufw allow 'Nginx HTTP'
```
```
sudo ufw status
```


If it is showing **inactive** that means your firewall is disabled 
Run this command 
```
sudo ufw enable
```

Now check the nginx status
```
sudo systemctl status nginx
```

It must show running. Now test the process.

You can access the default Nginx landing page to confirm that the software is running correctly by 
navigating to your server’s address. If you do not know your server’s IP address,
you can get it a few different ways.

``` 
ip addr show eth0 | grep inet | awk '{ print $2; }' | sed 's/\/.*$//' 
```

If you are making configuration changes, you can often reload Nginx without dropping
connections instead of restarting it. To do this, type the following:
```
sudo systemctl reload nginx
```

[To know more about nginx setup please follow this link](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-18-04)


#### Install Nodejs

Personally, I recommend installing node with **NVM**.

[Follow this link if you preferred another way of installing](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-20-04)

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh
```
```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```
```
source ~/.bashrc
```
```
nvm list-remote
```
Now install your desired version. Notice the **v** before version number.(v20.6.1)
```
nvm install vYOUR_VERSION
```
You can check your current installed versions.
```
nvm list
```
You can switch to your versions also.
```
nvm use v14.10.0
```


## Install PHP

```
sudo apt update -y
```
```
sudo apt upgrade -y
```
```
sudo apt install php8.1-fpm -y
```
```
sudo systemctl status php8.1-fpm
```
```
sudo nano /etc/nginx/sites-available/default
```

**Changes Portion**(Its not whole file, change only some part of it)

Add **index.php**, fpm change and deny htaccess block
```
index index.php index.html index.htm index.nginx-debian.html;

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;

    # Nginx php-fpm sock config:
    fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    # Nginx php-cgi config :
    # Nginx PHP fastcgi_pass 127.0.0.1:9000;
  }

# deny access to Apache .htaccess on Nginx with PHP, 
location ~ /\.ht {
    deny all;
}
```

```
sudo nginx -t
```
> nginx: the configuration file /etc/nginx/nginx.conf syntax is ok <br>
> nginx: configuration file /etc/nginx/nginx.conf test is successful<br>

If you get this message then your config is ok.
```
sudo systemctl restart nginx
```
```
sudo chmod -R 777 /var/www/html
```
```
echo "<?php phpinfo(); ?>" >> /var/www/html/info.php
```
Check if it is working :
```
http://YOUR_IP/info.php
```

Install some additional php extension
```
sudo apt install openssl php-bcmath php-curl php-json php-mbstring php-mysql php-tokenizer php-xml php-zip
```

[Follow this link](https://www.theserverside.com/blog/Coffee-Talk-Java-News-Stories-and-Opinions/Nginx-PHP-FPM-config-example)

## Install MySQL server
```
sudo apt update
```
```
sudo apt install mysql-server -y
```
```
sudo systemctl start mysql.service
```
Now login to mysql
```
sudo mysql
```
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root_password';
```
```
exit
```
You have finished setting up a password for the root user. Now login again to back to Then go back to using the default authentication method using this command.
```
mysql -u root -p
```
```
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
This will mean that you can once again connect to MySQL as your root user using the sudo mysql command.

```
sudo mysql_secure_installation
```
set strong passwords, and other options according to your needs. 

Now login again using sudo or using password
```
sudo mysql
```
OR
```
mysql -u root -p
```
Create an user with password
```
CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';
```

if it's showing error like **Your password does not satisfy the current policy requirements**
```
SHOW VARIABLES LIKE 'validate_password%';
```
You will see some variables related to passwords. Then set these variables like below:

```
SET GLOBAL validate_password.policy=LOW;SET GLOBAL validate_password.length=0;SET GLOBAL validate_password.mixed_case_count=0;SET GLOBAL validate_password.number_count=0;SET GLOBAL validate_password.special_char_count=0;
```
Now again try create User. It will be successfull. Grant priviledge now: 
```
GRANT CREATE, ALTER, DROP, INSERT, UPDATE, INDEX, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'moshiur'@'localhost' WITH GRANT OPTION;
```
To grant all privilege : (Risky)
```
GRANT ALL PRIVILEGES ON *.* TO 'moshiur'@'localhost' WITH GRANT OPTION;
```
Following this, it’s good practice to run the FLUSH PRIVILEGES command. This will free up any memory that the server cached as a result of the preceding CREATE USER and GRANT statements.
```
FLUSH PRIVILEGES;
```

```
exit
```
Login with your created user.
```
mysql -u moshiur -p
```
**Test mysql after exit**
```
systemctl status mysql.service
```
[Follown this link to deep dive](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)<br>
[Another helpful link](https://www.hostinger.com/tutorials/mysql/how-create-mysql-user-and-grant-permissions-command-line)


## Install composer 

[Get composer](https://getcomposer.org/download)

## Install git

Normally git is installed by default but if it not installed [Follow this link](https://www.atlassian.com/git/tutorials/install-git#linux) 

## Install ruby (if needed)
```
sudo apt install ruby ruby-dev -y
```
```
sudo gem install bundler
```


## Secure HTTPS with Certbot/Lets encrypt

```
sudo apt install certbot python3-certbot-nginx
```
```
sudo nano /etc/nginx/sites-available/your_domain.com
```
Change server_name part as
```
server_name your_domain.com www.your_domain.com;
```
```
sudo nginx -t
```
```
sudo systemctl reload nginx
```
**Allowing HTTPS Through the Firewall**
```
sudo ufw allow 'Nginx Full'
sudo ufw delete allow 'Nginx HTTP'
```
**Obtain certificate**
```
sudo certbot --nginx -d example.com -d www.example.com
```
Enter your email if you want. After submitting the certificate successfully obtained.

**Note:** If its not working properly that means you are not ointing domain to this ip properly. <br>
Please add @ and www both as A record. That's how I solved my issue.

**Certbot auto renewal test**
```
sudo systemctl status certbot.timer
```
```
sudo certbot renew --dry-run
```


[Follow this Link](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04)


