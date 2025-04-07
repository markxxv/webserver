# Install PHP


## To install php 7.4

Update system package list:
```
sudo apt-get update
apt-get install software-properties-common
add-apt-repository ppa:ondrej/php
apt-get update
```
Run installation
```
apt-get install php-pear php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-sqlite3 php7.4-xml php7.4-fpm php7.4-pgsql
```

## To install 8.2

```
sudo dpkg -l | grep php | tee packages.txt
sudo add-apt-repository ppa:ondrej/php 
sudo apt update
```
Run installation
```
apt-get install php-pear php8.2-curl php8.2-dev php8.2-gd php8.2-mbstring php8.2-zip php8.2-mysql php8.2-sqlite3 php8.2-xml php8.2-fpm php8.2-pgsql php8.2-intl php8.2-bcmath
```

8.3 Run installation
```
apt-get install php-pear php8.3-curl php8.3-dev php8.3-gd php8.3-mbstring php8.3-zip php8.3-mysql php8.3-sqlite3 php8.3-xml php8.3-fpm php8.3-pgsql php8.3-intl php8.3-bcmath
```

``` 8.4 Run installation
apt-get install php-pear php8.4-curl php8.4-dev php8.4-gd php8.4-mbstring php8.4-zip php8.4-mysql php8.4-sqlite3 php8.4-xml php8.4-fpm php8.4-pgsql php8.4-intl php8.4-bcmath
```

 ### If you want to change CLI version of php use this command: 
 
`sudo update-alternatives --set php /usr/bin/php7.4` or `sudo update-alternatives --set php /usr/bin/php8.2`

### Restart PHP service

`service php7.4-fpm restart` or `service php8.3-fpm restart`
