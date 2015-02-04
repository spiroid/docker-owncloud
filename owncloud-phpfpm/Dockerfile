FROM php:5.4-fpm
MAINTAINER Jonathan Dray <jonathan.dray@gmail.com>

# Install modules
RUN apt-get update && apt-get install -y \
    libmcrypt-dev libpng12-dev libfreetype6-dev libjpeg62-turbo-dev \
    && docker-php-ext-install iconv mcrypt zip mbstring \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-gd-dir=/usr/include/ \
    && docker-php-ext-install gd

CMD ["php-fpm"]
