FROM php:7.0-fpm
RUN apt-get update && apt-get install -y \
                libmcrypt-dev  \
                libicu-dev \
                mysql-client \
                libfreetype6-dev \
                libmcrypt-dev \
                libpng12-dev \
                libxml2-dev \
                libxslt-dev \
                libjpeg62-turbo-dev \
        && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
        && docker-php-ext-install -j$(nproc) gd \
        && docker-php-ext-install pdo \
        && docker-php-ext-install mysqli \
        && docker-php-ext-install pdo_mysql \
        && docker-php-ext-install mcrypt \
        && docker-php-ext-install intl \
        && docker-php-ext-install opcache \
        && docker-php-ext-install xml \
        && docker-php-ext-install soap \
        && docker-php-ext-install xsl \
        && docker-php-ext-install zip \
        && docker-php-ext-install json \
        && pecl install xdebug \
        && docker-php-ext-enable xdebug

# Configure
COPY php.ini /usr/local/etc/php/php.ini
COPY php-fpm.conf /usr/local/etc/
COPY ext-xdebug.ini /usr/local/etc/php/conf.d/ext-xdebug.ini

# Make sure the volume mount point is empty
RUN rm -rf /var/www/html/*

CMD ["php-fpm"]