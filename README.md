# Personal VPS Web Server 👨‍💻
Simple steps to configure your VPS web server 

## Must have stuff

* [How to install latest Nginx](https://github.com/markxxv/webserver/blob/main/nginx.md)
* [How to install latest MariaDB](https://github.com/markxxv/webserver/blob/main/mariadb.md)
* [How to install latest Node JS](https://github.com/markxxv/webserver/blob/main/nodejs.md)
* [Install & setup FireWall](https://github.com/markxxv/webserver/blob/main/firewall.md)

## Fast deploy by SSH
```
rsync --archive --compress --delete . user@8.8.8.8:/var/www/example.com/public/
```

Made with ♥️ in Sweden 🇸🇪
