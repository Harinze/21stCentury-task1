# WordPress Store Setup Guide
This guide provides step-by-step instructions to set up a WordPress store on your server.
url: http://135.181.203.59/

## Step 1: SSH into the Server

```bash
ssh deploy@<server ip address>
```
## Step 2: Install Required Dependencies
```
sudo apt update
sudo apt install nginx
sudo apt install mysql-server
sudo apt install php-fpm php-mysql
```
## Step 3: Configure Nginx
``` sudo nano /etc/nginx/sites-available/wordpress

# Add the following configuration:
# Replace <your server ip address> with your actual server IP address
server {
    listen 80;
    server_name <your server ip address>;

    root /var/www/wordpress;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}



```

## Step 4: Enable the WordPress Site
```sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
```
## Step 5: Restart Nginx
```
sudo systemctl restart nginx
```

## Step 6: Download and Install WordPress
```
cd /var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -zxvf latest.tar.gz
sudo mv wordpress/* wordpress/.htaccess ./
sudo chown -R www-data:www-data /var/www/html
sudo chmod -R 755 /var/www/html
```
## Step 7: Create the WordPress Database
```
sudo mysql -u root -p
Enter your MySQL root password when prompted, then execute the following SQL commands:
CREATE DATABASE wordpress;
CREATE USER 'xxxxxx'@'localhost' IDENTIFIED BY 'xxxxxx';
GRANT ALL PRIVILEGES ON wordpress.* TO 'xxxxxxx'@'localhost';
FLUSH PRIVILEGES;
EXIT;

```



