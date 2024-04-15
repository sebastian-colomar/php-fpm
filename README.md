# php-fpm

```
mkdir -p php-fpm
echo '<?php phpinfo();?>' | tee php-fpm/index.php
```
```
podman run --detach --name web --publish 8080:80 --rm httpd
curl -I localhost:8080/index.html
podman exec web grep -r ^LoadModule.mpm /usr/local/apache2/conf/httpd.conf
```
```
podman cp php-fpm/index.php web:/usr/local/apache2/htdocs/index.php
curl -I localhost:8080/index.php
```
```
podman kill web
podman run --detach --name web --publish 8080:80 --rm php:apache
podman cp php-fpm/index.php web:/var/www/html/index.php
curl -I localhost:8080/index.php
podman exec web ls /etc/apache2/mods-enabled | grep mpm.*load
```

