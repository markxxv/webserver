# How to install Latest MariaDB on Ubuntu 20.04 Focal

First of all you'll need to add verification key from MariaDB repository. Just run this command:

```
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
```

Then check latest version on [MariaDB official site](https://mariadb.org/download/) in my case it was a 10.6, but now it can be newest one

Open /etc/apt/sources.list add this lines at the end of file. Replace 10.6 with your wished version of MariaBD:

```
deb [arch=amd64,arm64,ppc64el] http://mirrors.accretive-networks.net/mariadb/repo/10.6/ubuntu focal main
```

Update your repositories:

```
sudo apt update
```

And install MariaDB:

```
sudo apt install mariadb-server
```

MariaDB service will start automatically, to verify it run:

```
sudo systemctl status mariadb
```

That's it! 🎉

[Back](https://github.com/markxxv/webserver)
