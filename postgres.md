# How to install Latest Postgres on Ubuntu 


Automated repository configuration: 
```
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```

Update the package lists:
```
sudo apt-get update
```

Install the latest version of PostgreSQL.
```
apt install postgresql
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
sudo pg_dropcluster --stop 16 main
sudo pg_createcluster --locale en_US.UTF-8 --start 16 main
```
> or pg_dropcluster --stop 16 main

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
