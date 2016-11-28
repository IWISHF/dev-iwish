# dev-iwish
This project provides services about develop documents and you can publish you knowledge that you want to shared.


# Setup Project

### Setup php (If you have not install php)
```sh
**step one (install php)**
sudo apt-get install -y php7.0
```
> explain -y
Automatic yes to prompts; assume "yes" as answer to all prompts and run non-interactively. If an undesirable situation,
such as changing a held package, trying to install a unauthenticated package or removing an essential package occurs then apt-get will abort. Configuration Item: APT::Get::Assume-Yes.

### Setup php extension
sudo apt-get install -y libapache2-mod-php7.0 php7.0-common php7.0-gd php7.0-mysql php7.0-mcrypt php7.0-curl php7.0-intl php7.0-xsl php7.0-mbstring php7.0-zip php7.0-bcmath php7.0-iconv php7.0-dev php7.0-cgi php7.0-redis php7.0-cli

### Setup mysql
You should create database named iwish or you liked.
but in /src/wp-config.php, we use iwish as default database

### Config nginx (Replace the root with your own project file path)
```
server {
    listen       80;
    server_name dev.iwish.com;
    root  /home/user/Desktop/my-github-file/dev-iwish/src;
    index index.html index.htm index.php;

    access_log /var/log/nginx/dev.iwish-access.log;
    error_log  /var/log/nginx/dev.iwish-error.log;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ .*\.(php|php5)?$ {
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        # or fastcgi_pass   127.0.0.1:9000;
        include        fastcgi_params;
    }

    location ~ /\.(ht|svn|git) {
            deny all;
    }
}
```

### Config Hosts
```
sudo subl /etc/hosts

# add config below
127.0.0.1 dev.iwish.com

```