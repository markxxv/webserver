# How to install Latest Nginx on Ubuntu 20.04 Focal 

First of one you need to add nginx offisial mainline repositories to your machine. 

 Open `/etc/apt/sources.list` add this lines at the end of file:

```
deb http://nginx.org/packages/mainline/ubuntu/ focal nginx
deb-src http://nginx.org/packages/mainline/ubuntu/ focal nginx
```

In order to verify the integrity of packages we need to import Nginx public key using the commands below:

```
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
```

> If you'll have error white second line execution like E: gnupg, gnupg2 and gnupg1 do not seem to be installed, but one of them is required for this operation.
>
> Just run this commant to fix it `apt-get install  gnupg2` and repeat last command

Now update repositories list:

```
sudo apt update
```

> If you'll get notification about `i386` , just ignore it. `Skipping acquire of configured file 'nginx/binary-i386/Packages' as repository 'http://nginx.org/packages/mainline/ubuntu focal InRelease' doesn't support architecture 'i386'` or alternatively you can replace first deb package with this `deb [arch=amd64,arm64] http://nginx.org/packages/mainline/ubuntu/ focal nginx`

Finally you are ready to install latest ngnix version:

```
sudo apt install nginx
```

Boom! Just run ngnix daemon and enjoy of best web server of ever!

```
sudo systemctl start nginx
```

