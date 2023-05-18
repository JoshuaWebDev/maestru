FROM php:7.4-apache

RUN apt update && apt install -y build-essential gcc g++ curl vim zip unzip \
    python-dev libpq-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libaio1
RUN docker-php-source extract
RUN docker-php-ext-install bcmath pdo_mysql
RUN docker-php-ext-configure gd --with-freetype --with-jpeg
RUN docker-php-ext-install -j "$(nproc)" gd
RUN docker-php-source delete

ENV USER joshua
ENV UID 1000

RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN chmod +x /usr/local/bin/composer

# Create system user to run Composer and Artisan Commands
RUN useradd -G www-data,root -u ${UID} -d /home/${USER} ${USER}
RUN mkdir -p /home/${USER}/.composer && chown -R ${USER}:${USER} /home/${USER}

RUN rm -rf /var/www/html

COPY . /var/www/maestru

WORKDIR /var/www/maestru

COPY ./apache/000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./apache/start-apache /usr/local/bin
COPY ./initial-configurations /usr/local/bin

RUN chmod +x /usr/local/bin/start-apache
RUN chmod +x /usr/local/bin/initial-configurations
RUN a2enmod rewrite
