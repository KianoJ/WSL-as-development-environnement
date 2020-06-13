# Install NGINX

```
sudo apt install nginx -y
```

## Allow PHP files

Open `default` file from `/etc/nginx/sites-available/` and add `index.php` in the list 

```
# Default server configuration
#
server {
        listen 80 default_server;
        listen [::]:80 default_server;

		.
		.
		.

        # Add index.php to the list if you are using PHP
        index index.php index.html index.htm index.nginx-debian.html;
```

Uncoment `location ~ \.php$ {` section

```
location ~ \.php$ {
		include snippets/fastcgi-php.conf;
		# With php-fpm (or other unix sockets):
		fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
		# With php-cgi (or other tcp sockets):
		fastcgi_pass 127.0.0.1:9000;
}
```