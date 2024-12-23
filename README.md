# Brainstorm


sudo apt install mysql-server mysql-client -y
sudo systemctl enable mysql

sudo mysql_secure_installation

#BY default the SQL root passwd is empty 

select user,authentication_string,plugin,host from mysql.user;

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '<passwd>';

#Install php-fpm php-mysql

sudo apt install php-fpm php-mysql -y

#COnfiguring nginx

cd /etc/nginx/sites-available/

create a new file with your domain name

vi kopsakvp.site

-------------
server {
        listen 80;
        root /var/www/html;
        index index.php index.html index.htm index.nginx-debian.html;
        server_name jgogoi.online;

        location / {
                try_files $uri $uri/ =404;
        }

        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        }

        location ~ /\.ht {
                deny all;
        }
}


Make softlink 

sudo ln -s /etc/nginx/sites-available/kopsakvp.site /etc/nginx/sites-enabled/

unlink default

check if the congifuration is correct 

sudo nginx -t

#install phpmyadmin

sudo apt install phpmyadmin -y

#link the phpmyadmin to the user dir /var/www/html

sudo ln -s /usr/share/phpmyadmin/ /var/www/html/phpmyadmin