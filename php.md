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

To install 8.1

```
apt-get install php-pear php8.1-curl php8.1-dev php8.1-gd php8.1-mbstring php8.1-zip php8.1-mysql php8.1-sqlite3 php8.1-xml php8.1-fpm php8.1-pgsql
```

### Restart PHP service

`service php7.4-fpm restart` or `service php8.1-fpm restart`
