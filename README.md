# Assessment-Sysadmin
## Tujuan
Menilai kemampuan kandidat dalam menginstal, mengonfigurasi, dan mengelola server web menggunakan Nginx, PHP 8.0, MySQL 8.0, serta mengelola website berbasis WordPress dan Laravel.

# Alat dan Bahan 
Internet
End Device

# Instalasi dan Konfigurasi:
## Instal Nginx.
### Open terminal ssh
ssh ubuntu@16.78.111.195
### cek host komputer : 
hostname && hostname -f
### install ntp : 
apt-get install ntp -y
### kemudian rekonfigurasi ntp : 
dpkg-reconfigure locales
### tambahkan zona Indonesia
### set lokasi : 
locale-gen
### cek ntp : 
ntpq -p ,pastikan nilai 0
### set bashrc : 
nano /etc/bash.bashrc ,kemudian hilangan pasar complitenya untuk aktifkan.
## Install Nginx : 
apt-get install nginx -y
## Instal PHP 8.0. : 
apt--get install php8.0 php8.0-mysql php8.0-curl php8.0-cli php8.0-gd php8.0-fpm php8.0-mbstring php8.0-imagick php8.0-xmlrpc php8.0-xml php8.0-mcrypt php8.0-intl php-pear
## Instal MySQL 8.0 : 
apt-get install mysql-server-8.0
### ketik : 
mysql_secure_installation
#### kemudian pilih :
Y (all)
### selanjutnya ganti password mysqlnya dengan karakter panjang : 
5ECx24Da1oEo8NIK
### kemudian login mysql : 
mysql -u root -p
### buat database : 
CREATE database wordpress
### buat database user login wordpress :
CREATE USER 'wordpress_user'@'localhost' IDENTIFIED BY 'Miesedap0077# ';
GRANT ALL PRIVILEGES ON wordpress* TO 'wordpress_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;

## Konfigurasi Virtual Host
### Virtual Hosts:
cd /etc/nginx/site-available
nano Laravel
### Tambahkan syntck :
server {
    server_name laravel.muchib.efs.my.id www.laravel.muchib.efs.my.id;

    root /var/www/Laravel/efs/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
### Kemudian buat virtualhost wordpress :
nano WordPress
server {
    server_name wordpress.muchib.efs.my.id www.wordpress.muchib.efs.my.id;

    root /var/www/WordPress;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

## Instalasi dan Konfigurasi WordPress:
mkdir var/www/Wordpress
wget https://wordpress.org/latest.zip
apt-get install unzip -y
unzip latest.zip
### buka browser :
wordpress.muchib.efs.my.id
konfigurasi database
submit
konfigurasi website profile dan login wordpress.
masuk dashboard wordpress
install plugin WFH sebagai firewall keamanan.
testing.
## Instalasi Laravel:
### buka folder Laravel :
cd /var/www/Laravel
install composer
buat proyek laravel nama efs
hak akses chmod -R 755 *
hak akses chown -R www-data:www-data *
kemudian testing : laravel.muchib.efs.my.id

## Konfigurasi PHP:
buat oncek.php di /var/www/html buat testing.
<?php
phpinfo();
>?

masuk ke php.ini kemudian ganti menjadi nilai berikut.

upload_max_filesize = 100M
post_max_size = 100M
memory_limit = 512M

## Manajemen Partisi:
memory usage total 10GB.
ketik perintah df -h
berhasil

## Akses Publik:
Akses wordpress : wordpress.muchib.efs.my.id
Akses Laravel : laravel.muchib.efs.my.id

## Keamanan Tambahan:
Untuk mengamankan akses menggunakan 443.
### Konfigurasi HTTPS Install Cherbot:
sudo apt update
sudo apt install certbot python3-certbot-nginx
### kemudian generate RSA
sudo certbot --nginx -d wordpress.muchib.my.id
### pilih 
Y (all)
### kemduian generate RSA selanjutnya.
sudo certbot --nginx -d laravel.muchib.efs.my.id
### pilih 
Y (all)


## Akses Login Database MySQL :

username : wordpress_user
pass : Miesedap0077# 

## Akses wordpress :
username : admin
pass : MtZxQGvwC)@v&(p$bN
