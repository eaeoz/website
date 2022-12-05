+++
title = "Alpine Php Docker CLI"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-11T05:00:00Z
description = "alpine php docker"
categories = ["docker"]
type = "post"

+++
```
docker run --name websrv -p 8088:80 joseluisq/php-fpm:8.1 sh -c "echo <?php phpinfo();' > index.php; php -S [::]:80 -t ."
```
or

```
cd /
mkdir w2
cd w2
sudo nano index.php
<?php
phpinfo();
?>

sudo docker run --name websrv -p 8088:80 joseluisq/php-fpm:8.1 sh -c "echo '<?php phpinfo();' > index.php; php -S [::]:80 -t ." -v /w2:/var/www/html
```

https://hub.docker.com/r/joseluisq/php-fpm/

test 8.0 and 7.4 versions
```
docker run --rm -p 8088:80 joseluisq/php-fpm:8.0 sh -c "echo '<?php phpinfo();' > index.php; php -S [::]:80 -t ."
```
or
```
docker run --rm -p 8088:80 joseluisq/php-fpm:7.4 sh -c "echo '<?php phpinfo();' > index.php; php -S [::]:80 -t ."
```
**erseco/alpine-php-webserver**
```
docker run -p 80:8080 -v ~/my-codebase:/var/www/html erseco/alpine-php-webserver
```
or
```
sudo docker run --name webserver -p 4534:8080 -v /docker/my-codebase:/var/www/html erseco/alpine-php-webserver
```





