# Install Firewall UFW 🔥

Install package

```
apt install ufw
```

Add Exeptions for Nginx

```
vi /etc/ufw/applications.d/nginx.ini
```

Past 

```
[Nginx HTTP]
title=Web Server
description=Enable NGINX HTTP traffic
ports=80/tcp

[Nginx HTTPS] \
title=Web Server (HTTPS) \
description=Enable NGINX HTTPS traffic
ports=443/tcp

[Nginx Full]
title=Web Server (HTTP,HTTPS)
description=Enable NGINX HTTP and HTTPS traffic
ports=80,443/tcp
```

Then check

```
ufw app list
```

Allow services

```
ufw allow 'Nginx Full'
ufw allow 'OpenSSH'
```

Start firewall

```
ufw enable
```

Check firewall status


```
ufw status
```

Open port for cpecific ip

```
sudo ufw allow from 10.0.0.46 proto tcp to any port 5432
```

And remove this

```
sudo ufw delete allow from 10.0.0.46 proto tcp to any port 5432
```

Now your server is secure as hell 🔥

[Back](https://github.com/markxxv/webserver)
