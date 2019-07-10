FROM php:7.2-apache
COPY php.ini /usr/local/etc/php/
RUN apt-get update \
  && apt-get install -y wget libpq-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libmcrypt-dev libbz2-dev libzip-dev \
  && pecl install mcrypt-1.0.2 \
  && docker-php-ext-enable mcrypt \
  && docker-php-ext-install pdo_pgsql mbstring gd iconv zip bz2 opcache

# Create new web user for apache and grant sudo without password
RUN useradd web -d /var/www -g www-data -s /bin/bash
RUN usermod -aG sudo web
RUN echo 'web ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Add sudo to www-data
RUN echo 'www-data ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# Set timezone to Europe/Paris
RUN echo "Europe/Paris" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata

EXPOSE 80 9000

# Install xdebug. We need at least 2.4 version to have PHP 7 support.
RUN cd /tmp/ && wget http://xdebug.org/files/xdebug-2.6.1.tgz && tar -xvzf xdebug-2.6.1.tgz && cd xdebug-2.6.1/ && phpize && ./configure --enable-xdebug --with-php-config=/usr/local/bin/php-config && make && make install
RUN cd /tmp/xdebug-2.6.1 && cp modules/xdebug.so /usr/local/lib/php/extensions/no-debug-non-zts-20170718/
RUN echo 'zend_extension = /usr/local/lib/php/extensions/no-debug-non-zts-20170718/xdebug.so' >> /usr/local/etc/php/php.ini
RUN touch /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_enable=1' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_autostart=0' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_connect_back=0' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_port=9000' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_log=/tmp/php7-xdebug.log' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
  echo 'xdebug.remote_host=docker_host' >> /usr/local/etc/php/conf.d/xdebug.ini &&\
echo 'xdebug.idekey=PHPSTORM' >> /usr/local/etc/php/conf.d/xdebug.ini

COPY virtual.conf /etc/apache2/sites-available/
RUN mkdir -p /var/log/httpd/php7.localdomain
RUN echo "ServerName localhost" | tee /etc/apache2/conf-available/fqdn.conf
RUN a2enconf fqdn && a2enmod rewrite expires && a2dissite 000-default && a2ensite virtual
RUN service apache2 start
RUN curl -sS https://getcomposer.org/installer | php \
  && mv composer.phar /usr/local/bin/composer
