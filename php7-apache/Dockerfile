#
# php7-apache
#
FROM fedora:22

# Update distribution
RUN dnf -y update; dnf clean all

# Need Apache in simplest way
RUN dnf -y install httpd; \
    dnf clean all
RUN mkdir -p /var/www/html
RUN mkdir -p /var/log/httpd

# Install remi's repository
RUN dnf -y install wget
RUN wget http://rpms.remirepo.net/fedora/remi-release-22.rpm
RUN dnf -y install remi-release-22.rpm

# Install PHP 7.0 from remi's repository
RUN dnf --enablerepo=remi --enablerepo=remi-test -y install \
  php70 \
  php70-php \
  php70-php-common \
  php70-php-cli \
  php70-php-devel \
  php70-php-gd \
  php70-php-mbstring \
  php70-php-mcrypt \
  php70-php-pecl-memcached \
  php70-php-mysqlnd \
  php70-php-pdo \
  php70-php-pgsql \
  php70-php-xml; \
  dnf clean all

# Copy apache run script
ADD run-apache.sh /run-apache.sh
RUN chmod -v +x /run-apache.sh

# Configure PHP using custom VirtualHost configuration
ADD virtualhost.conf /etc/httpd/conf.d/virtualhost.conf

# Create Apache test page
WORKDIR /src
RUN echo "<?php phpinfo();" > /src/index.php
RUN rm -rf /var/www/html; ln -s /src /var/www/html

# Done
EXPOSE 80
CMD ["/run-apache.sh"]
