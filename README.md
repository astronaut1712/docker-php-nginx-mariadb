# docker nginx with php5-fpm

[![](https://images.microbadger.com/badges/image/astronaut1712/nginx-php.svg)](https://microbadger.com/images/astronaut1712/nginx-php "Get your own image badge on microbadger.com")

## How to use

```
docker run -d --name web-php -p 80:80 -p 443:443 astronaut1712/nginx-php:5
```

## Use with MariaDB

Create a `docker-compose.yml` follow by:

```
db:
  image: mariadb
  environment:
    - MYSQL_ROOT_PASSWORD=Y0urP@ssW0rd
  ports:
    - "3306:3306"
  volumes:
    - ./mariadb/data:/var/lib/mysql # To store MariaDB database data
    - ./mariadb/conf:/etc/mysql/conf.d # To store more configuration for MariaDB

web:
  image: astronaut1712/nginx-php:5
  ports:
    - "80:80"
    - "443:443"
  links:
    - db:db
  volumes:
    - ./nginx/etc/ssl:/etc/nginx/ssl # To store ssl configuration for nginx
    - ./nginx/vhost:/etc/nginx/sites-enabled # To store virtual host configuration
    - ./nginx/src:/var/www # To store root document
    - ./nginx/logs:/var/log/nginx # To store nginx log
```

And then run `docker-compose up` to use it.
