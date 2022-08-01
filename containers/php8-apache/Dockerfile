FROM php:8.0-apache

RUN a2enmod rewrite
RUN a2enmod headers

RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/local/bin/composer \
    && curl -sL https://deb.nodesource.com/setup_12.x  | bash

RUN apt-get install -y vim git unzip curl wget make
RUN apt-get install -y zlib1g-dev libpng-dev libzip-dev libjpeg62-turbo-dev libfreetype6-dev libzip-dev libonig-dev libxrender1 \
                       libfontconfig fontconfig libfontconfig-dev

RUN wget -N https://sourceforge.net/projects/libpng/files/libpng15/1.5.30/libpng-1.5.30.tar.gz/download -O /usr/share/libpng-1.5.30.tar.gz && tar xzf /usr/share/libpng-1.5.30.tar.gz
RUN cd libpng-1.5.30 && ./configure --prefix=/usr && make install

# Install extensions
RUN docker-php-ext-install gd
RUN docker-php-ext-install zip
RUN docker-php-source delete

RUN apt-get update && apt-get upgrade -y

RUN groupadd -g 1000 www
RUN useradd -u 1000 -ms /bin/bash -g www www

#RUN chown -R www-data:www-data /var/www/html
RUN chmod -R g+rw /var/www/html

#Login with current user www
USER www