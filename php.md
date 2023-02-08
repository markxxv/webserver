# Install PHP

Update system package list:
```
sudo apt-get update
```

Tool for update repositories
```
apt-get install software-properties-common
```

add repository
```
add-apt-repository ppa:ondrej/php
```

update your package list:
```
apt-get update
```

To install php 7.4

```
apt-get install php-pear php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-sqlite3 php7.4-xml php7.4-fpm php7.4-pgsql
```

To install 8.2

```
apt-get install php-pear php8.2-curl php8.2-dev php8.2-gd php8.2-mbstring php8.2-zip php8.2-mysql php8.2-sqlite3 php8.2-xml php8.2-fpm php8.2-pgsql
```

 ### If you want to change CLI version of php use this command: 
 
`sudo update-alternatives --set php /usr/bin/php7.4` or `sudo update-alternatives --set php /usr/bin/php8.2`

### Restart PHP service

`service php7.4-fpm restart` or `service php8.2-fpm restart`
