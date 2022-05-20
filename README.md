# Personal VPS Web Server setup & administration 👨‍💻
Simple steps to setup your VPS web server on Ubuntu 20.04 LTS

## Must have stuff

* [How to install latest Nginx](https://github.com/markxxv/webserver/blob/main/nginx.md)
* [How to install latest MariaDB](https://github.com/markxxv/webserver/blob/main/mariadb.md)
* [How to install latest Postgres SQL](https://github.com/markxxv/webserver/blob/main/postgres.md)
* [How to install latest Node JS](https://github.com/markxxv/webserver/blob/main/nodejs.md)
* [Install & setup FireWall](https://github.com/markxxv/webserver/blob/main/firewall.md)
* [Install PHP](https://github.com/markxxv/webserver/blob/main/php.md)

## Fast deploy by SSH
```
rsync --archive --compress --delete . user@8.8.8.8:/var/www/example.com/public/
```

### Install Your Own VPN

```
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```
Then use generataed file to connect from your client 

Made with ♥️ in Sweden 🇸🇪
