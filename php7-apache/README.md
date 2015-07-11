# php7-apache

A Docker image for Apache and PHP 7.0 based on Fedora 22.

This container use the (PHP 7.0 SCL from Rémi)[http://blog.famillecollet.com/post/2015/03/25/PHP-7.0-as-Software-Collection].


## Build the image: 

```
# docker build --rm -t eliep/fedora-apache-php-7 .
```

## Start

### Background
To start a container in the background accessible on localhost:8000
```
# docker run -d -p 8000:80 eliep/fedora-apache-php-7
```

### Mount your files
The virtualhost.conf file expose the /src directory. As a default, it only contains an index.php file with a phpinfo(). You can use a volume to overrides this directory:
```
# docker run -d -v /your/php/directory:/src -p 8000:80 eliep/fedora-apache-php-7
```

### PHP CLI
To start a container with an interactive shell 
```
# docker run -it -p 8000:80 eliep/fedora-apache-php-7 /bin/bash
```

From their, you can use PHP 7 cli, with the regular php command.
```
# php -v
```

You can also start apache with:
```
# run-apache.sh
```

After that, use `apachectl -k [stop|start|restart]`

