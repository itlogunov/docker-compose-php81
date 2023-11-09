FROM php:8.1-fpm

RUN apt-get update && apt-get install -y \
      apt-utils \
      libpq-dev \
      libpng-dev \
      libjpeg-dev \
      libwebp-dev \
      libzip-dev \
      zip unzip \
      libfreetype6-dev \
      libjpeg62-turbo-dev \
      webp \
      jpegoptim \
      optipng \
      curl \
      sendmail \
      git && \
      pecl install memcache && \
      docker-php-ext-enable memcache && \
      docker-php-ext-install opcache && \
      docker-php-ext-install mysqli && \
      docker-php-ext-install pdo_mysql && \
      docker-php-ext-install bcmath && \
      docker-php-ext-install gd && \
      docker-php-ext-install zip && \
      docker-php-ext-configure gd --with-freetype --with-jpeg --with-webp && \
      docker-php-ext-install -j$(nproc) gd && \
      apt-get clean && \
      rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY ./_docker/config/php/conf.d/php.ini /usr/local/etc/php/conf.d/php.ini
COPY ./_docker/config/php/conf.d/sendmail.ini /usr/local/etc/php/conf.d/sendmail.ini

# composer
ENV COMPOSER_ALLOW_SUPERUSER=1
RUN curl -sS https://getcomposer.org/installer | php -- \
    --filename=composer \
    --install-dir=/usr/local/bin

WORKDIR /var/www