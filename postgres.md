# How to install Latest Postgres on Ubuntu 20.04 Focal


Create the file repository configuration:
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
```

Import the repository signing key:
```
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```

Update the package lists:
```
sudo apt-get update
```

Install the latest version of PostgreSQL.
> If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql':
```
sudo apt-get -y install postgresql
```

That's it! 🎉


## Create User & Database

Switch to pg console:
```
sudo -u postgres psql
```

Create user interactive
```
sudo -u postgres createuser --interactive -P
```

### Set UTF8

```
sudo pg_dropcluster --stop 14 main
sudo pg_createcluster --locale en_US.UTF-8 --start 14 main
```
> or pg_dropcluster --stop 14.1 main

### Create database
```
CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;
```

### Alternativley you can create only your database in UTF-8

```
CREATE DATABASE myawesomr_db WITH ENCODING='UTF8' LC_CTYPE='en_US.UTF-8' LC_COLLATE='en_US.UTF-8' OWNER=aura31aty2k_user TEMPLATE=template0 CONNECTION LIMIT=-1;
```

### To show all databases
```
\l
```


[Back](https://github.com/markxxv/webserver)
