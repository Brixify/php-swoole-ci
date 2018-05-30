FROM php:7.2-alpine
MAINTAINER "Bence Gazder"
LABEL maintainer="bence.gazder@brixify.com"

ENV COMPOSER_VERSION 1.6.5

# install dependencies
RUN apk add --no-cache \
    bash \
    supervisor \
    dcron \
    ca-certificates \
    freetype \
    libssl1.0 \
    libpng \
    libjpeg-turbo \
    libmcrypt \
    curl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
	  openssl-dev \
	  icu-dev \
    icu-libs \
    $PHPIZE_DEPS \
    nano \
    git \
    openssh-client \
# configure extensions
    && docker-php-ext-configure intl --enable-intl \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
# install extensions
    && docker-php-ext-install \
    mbstring \
    intl \
    curl \
    json \
    pdo_mysql \
    exif \
    zip \
    gd \
    bcmath \
# pecl extensions
    && pecl install swoole \
    && docker-php-ext-enable swoole \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb \
    && pecl install xdebug \
    && docker-php-ext-enable xdebug \
# composer
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=${COMPOSER_VERSION} \
    && chmod +x /usr/local/bin/composer \
# minio/s3 client
    && curl -o mc https://dl.minio.io/client/mc/release/linux-amd64/mc \
    && chmod +x ./mc \
    && mv ./mc /usr/local/bin \
# set up composer
    && composer global require hirak/prestissimo --profile --prefer-dist --no-progress --no-suggest --optimize-autoloader --no-interaction \
# cleanup
    && docker-php-source delete \
    && apk del \
    curl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
	  openssl-dev \
	  icu-dev \
    && apk info \
    && php -i \
    && php -v

CMD ["php", "-v"]
