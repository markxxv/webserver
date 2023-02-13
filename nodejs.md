# Node JS

To install latest Node JS just replace the version number in my command with the desired one

```
wget https://nodejs.org/dist/v18.4.0/node-v18.4.0-linux-x64.tar.gz
```

And install

```
sudo tar -C /usr/local --strip-components 1 -xzf node-v18.4.0-linux-x64.tar.gz
```

Boom! 🎉 That's it! 

Check it 

```
node -v
```

## Upgrade Node JS Version

Use n module from npm in order to upgrade node

```
sudo npm cache clean -f
sudo npm install -g n
sudo n stable
```
To upgrade to latest version (and not current stable) version, you can use

```
sudo n latest
```

[Back](https://github.com/markxxv/webserver)
