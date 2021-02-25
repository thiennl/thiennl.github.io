

**0. Snipe-IT là gì**

Website: https://snipeitapp.com/

**1. Cài đặt nginx**

- Gỡ apache2 nếu có  
- Cài nginx  
```bash
root@dinguyen:~#apt update  
root@dinguyen:~#apt install nginx
root@dinguyen:~#systemctl start nginx
root@dinguyen:~#system enable nginx
root@dinguyen:~#systemctl status nginx
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2021-02-23 08:20:36 UTC; 6h left
       Docs: man:nginx(8)
   Main PID: 862 (nginx)
      Tasks: 3 (limit: 4586)
     Memory: 9.6M
     CGroup: /system.slice/nginx.service
             ├─862 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
             ├─863 nginx: worker process
             └─864 nginx: worker process

Feb 23 08:20:35 snipeit systemd[1]: Starting A high performance web server and a reverse proxy server...
Feb 23 08:20:36 snipeit systemd[1]: Started A high performance web server and a reverse proxy server.
root@dinguyen:~#
```  
**2. Cài đặt mariadb**
```bash
root@dinguyen:~# apt install mariadb-server mariadb-client
root@dinguyen:~#systemctl start mariadb
root@dinguyen:~#systemctl enable mariadb
root@dinguyen:~#systemctl status mariadb
root@dinguyen:~#systemctl status mariadb
● mariadb.service - MariaDB 10.3.25 database server
     Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2021-02-23 08:20:37 UTC; 6h left
       Docs: man:mysqld(8)
             https://mariadb.com/kb/en/library/systemd/
   Main PID: 956 (mysqld)
     Status: "Taking your SQL requests now..."
      Tasks: 31 (limit: 4586)
     Memory: 94.1M
     CGroup: /system.slice/mariadb.service
             └─956 /usr/sbin/mysqld

Feb 23 08:20:35 snipeit systemd[1]: Starting MariaDB 10.3.25 database server...
Feb 23 08:20:36 snipeit mysqld[956]: 2021-02-23  8:20:36 0 [Note] /usr/sbin/mysqld (mysqld 10.3.25-MariaDB-0ubuntu0.20.04.1) starting as process 956 ...
Feb 23 08:20:36 snipeit mysqld[956]: 2021-02-23  8:20:36 0 [Warning] Could not increase number of max_open_files to more than 16384 (request: 32184)
Feb 23 08:20:37 snipeit systemd[1]: Started MariaDB 10.3.25 database server.
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1066]: Upgrading MySQL tables if necessary.
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1070]: Looking for 'mysql' as: /usr/bin/mysql
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1070]: Looking for 'mysqlcheck' as: /usr/bin/mysqlcheck
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1070]: This installation of MySQL is already upgraded to 10.3.25-MariaDB, use --force if you still need to run mysql_upgrade
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1081]: Checking for insecure root accounts.
Feb 23 08:20:37 snipeit /etc/mysql/debian-start[1085]: Triggering myisam-recover for all MyISAM tables and aria-recover for all Aria tables
root@dinguyen:~
```
```bash
root@dinguyen:~#mysql_secure_installation
Enter current password for root (enter for none): Enter
Set root password? [Y/n]: Y
New password: Enter password
Re-enter new password: Repeat password
Remove anonymous users? [Y/n]: Y
Disallow root login remotely? [Y/n]: Y
Remove test database and access to it? [Y/n]:  Y
Reload privilege tables now? [Y/n]:  Y
```  
**3. Tạo Snipe-IT database**
```sql
root@dinguyen:~#mysql -u root -p
CREATE DATABASE snipeit;
CREATE USER 'snipeit'@'localhost' IDENTIFIED BY 'Dinguyen@2021';
GRANT ALL ON snipeit.* TO 'snipeit'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```  
**4. Cài đặt PHP**
- Cài đăht php và các modules  
```bash
root@dinguyen:~# apt install php-fpm php-common php-gmp php-curl php-intl php-mbstring php-xmlrpc php-mysql php-gd php-bcmath php-xml php-cli php-zip php-ldap
```
- Set các tham số trong file php.ini  
```bash
root@dinguyen:~# vi /etc/php/7.4/fpm/php.ini
```
```text
file_uploads = On
allow_url_fopen = On
short_open_tag = On
cgi.fix_pathinfo = 0
memory_limit = 256M
upload_max_filesize = 100M
max_execution_time = 360
max_input_vars = 1500
date.timezone = Asia/Ho_Chi_Minh
```  
**5. Download và cài đặt Snipe-IT**
```bash
root@dinguyen:~#apt install curl git
root@dinguyen:~#curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
cd /var/www/
root@dinguyen:~#git clone https://github.com/snipe/snipe-it snipeit
root@dinguyen:~#cp /var/www/snipeit/.env.example /var/www/snipeit/.env
```  
- Sửa file .env  
```bash
root@dinguyen:~# vi /var/www/snipeit/.env
```
```text
# --------------------------------------------
# REQUIRED: BASIC APP SETTINGS
# --------------------------------------------
APP_ENV=production
APP_DEBUG=false
APP_KEY=ChangeMe
APP_URL=dinguyen.com
APP_TIMEZONE='UTC'
APP_LOCALE=en
MAX_RESULTS=500

# --------------------------------------------
# REQUIRED: DATABASE SETTINGS
# --------------------------------------------
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=snipeit
DB_USERNAME=snipeit
DB_PASSWORD=Dinguyen@2021
DB_PREFIX=null
DB_DUMP_PATH='/usr/bin'
DB_CHARSET=utf8mb4
DB_COLLATION=utf8mb4_unicode_ci

# --------------------------------------------
# OPTIONAL: SSL DATABASE SETTINGS
```
```bash
root@dinguyen:~#cd /var/www/snipeit
root@dinguyen:~#composer install --no-dev --prefer-source
root@dinguyen:~#php artisan key:generate
Do you really wish to run this command? (yes/no) [no]:
 > yes
root@dinguyen:~#chown -R www-data:www-data /var/www/snipeit/
root@dinguyen:~#chmod -R 755 /var/www/snipeit/
```  
- Sửa file /etc/nginx/sites-available/default
```bash
root@dinguyen:~# vi /etc/nginx/sites-available/default
```
```text
server {
        listen 80 default_server;
        listen [::]:80 default_server;

        root /var/www/snipeit/public;
        index  index.php;
        server_name _;

        location / {
                try_files $uri $uri/ /index.php$is_args$args;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php-fpm.sock;
                include fastcgi_params;
                fastcgi_intercept_errors on;
         }
}
```
- Restart nginx
```bash
root@dinguyen:~#systemctl restart nginx.
```
*... to be continued*