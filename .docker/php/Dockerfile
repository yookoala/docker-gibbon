FROM php:7.2.12-fpm

RUN apt-get update \
    && apt-get install -y --no-install-recommends vim curl debconf subversion git apt-transport-https apt-utils \
    build-essential locales acl mailutils wget zip unzip \
    gnupg gnupg1 gnupg2

COPY php.ini /etc/php/7.2.12/php.ini
COPY php-fpm-pool.conf /etc/php/7.2.12/pool.d/www.conf

RUN curl -sSk https://getcomposer.org/installer | php -- --disable-tls && \
   mv composer.phar /usr/local/bin/composer

RUN groupadd dev -g 999
RUN useradd dev -g dev -d /home/dev -m

RUN rm -rf /var/lib/apt/lists/*

RUN apt-get update
RUN apt-get install -qy git zip unzip zlib1g-dev gettext 
RUN docker-php-ext-install zip gettext pdo_mysql > /dev/null
RUN echo "en.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    echo "fr_FR.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen

WORKDIR /home/www/

EXPOSE 9000
CMD ["php-fpm"]