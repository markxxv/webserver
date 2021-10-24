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


```
sudo -u postgres psql
```

Create database
```
CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;
```

To show all databases
```
\l
```


[Back](https://github.com/markxxv/webserver)
