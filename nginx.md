# How to install Latest Nginx on Ubuntu 20.04 Focal 

First of one you need to add nginx offisial mainline repositories to your machine. 

 Open `/etc/apt/sources.list` add this lines at the end of file:

```
deb http://nginx.org/packages/mainline/ubuntu/ focal nginx
deb-src http://nginx.org/packages/mainline/ubuntu/ focal nginx
```

In order to verify the integrity of packages we need to import Nginx public key using the commands below:

```
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
```

> If you'll have error white second line execution like E: gnupg, gnupg2 and gnupg1 do not seem to be installed, but one of them is required for this operation.
>
> Just run this commant to fix it `apt-get install  gnupg2` and repeat last command

Now update repositories list:

```
sudo apt update
```

> If you'll get notification about `i386` , just ignore it. `Skipping acquire of configured file 'nginx/binary-i386/Packages' as repository 'http://nginx.org/packages/mainline/ubuntu focal InRelease' doesn't support architecture 'i386'` or alternatively you can replace first deb package with this `deb [arch=amd64,arm64] http://nginx.org/packages/mainline/ubuntu/ focal nginx`

Finally you are ready to install latest ngnix version:

```
sudo apt install nginx
```

Boom! Just run ngnix daemon and enjoy of best web server of ever!

```
sudo systemctl start nginx
```

⚠️ To prevent access errors change /etc/nginx/nginx.conf user from `user nginx` to user `www-data`

✅ Tip > for add virtual hosts in the end of `/etc/nginx/nginx.conf` add  `include /etc/nginx/sites-enabled/*;`

## Example Host for PHP App

```
server {
    listen   80; ## listen for ipv4; this line is default and implied
    listen   [::]:80 default ipv6only=on; ## listen for ipv6

    root /var/www/default;
    index index.php index.html index.htm;
    server_name 45.12.19.173;
         

    # Disable sendfile as per https://docs.vagrantup.com/v2/synced-folders/virtualbox.html
    sendfile off;

    # Security - Hide nginx version number in error pages and Server header
    server_tokens off;

    # reduce the data that needs to be sent over network
    gzip on;
    gzip_min_length 10240;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain text/css text/xml application/json text/javascript application/x-javascript application/xml;
    gzip_disable "MSIE [1-6]\.";


    location / {
        # First attempt to serve request as file, then
        # as directory, then fall back to index.php
        try_files $uri $uri/ /index.php?$query_string $uri/index.html;
    }

    # redirect server error pages to the static page /50x.html
    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    } 

    # pass the PHP scripts to FastCGI server listening on socket
    location ~ \.php$ {
        try_files $uri $uri/ /index.php?$query_string;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/run/php/php8.3-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }

    # deny access to . files, for security
    location ~ /\. {
        log_not_found off;
        deny all;
    }

}
```


You can link www and sites enabled folders to your home directory

```
ln -s /etc/nginx/sites-enabled /root
ln -s /var/www /root
```

## Increase timeout 

```
	keepalive_timeout 65;
	client_max_body_size 1024M;
```

Basic example for laravel app with php execution protection
```
server {
    server_name www.smbureau.fr;
    return 301 $scheme://smbureau.fr$request_uri;
}

server {
    listen 80;
    server_name smbureau.fr;

    root /var/www/smbureau.fr/public;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    # ❌ deny any PHP file eexecution
    location ~ \.php$ {
        return 404;
    }

    # ✅ allow only frontcontroller
    location = /index.php {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.4-fpm.sock;
    }

    # ❌ deny hiiden files
    location ~ /\. {
        deny all;
    }
}
```

[Back](https://github.com/markxxv/webserver)
