# musiko
Musiko website

h2. Installation :

git clone https://github.com/lecler-i/musiko
cd musiko
composer install

h3. Nginx config :

server {
    listen 80;

    root /var/www/nginx/musiko/public;
    index index.php index.html index.htm;

    server_name musiko.localhost;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php5-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
