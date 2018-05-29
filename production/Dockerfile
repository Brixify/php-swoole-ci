FROM php:7.2-alpine
MAINTAINER "Bence Gazder"
LABEL maintainer="bence.gazder@brixify.com"

# install dependencies
RUN apk add --no-cache \
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
    && pecl install swoole \
    && docker-php-ext-enable swoole \
    && pecl install mongodb \
    && docker-php-ext-enable mongodb \
# cleanup
    && docker-php-source delete \
    && apk del \
    curl-dev \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
	openssl-dev \
	icu-dev \
	$PHPIZE_DEPS \
	&& rm /usr/local/bin/phpdbg \
	&& rm -rf /usr/src/ \
	&& apk info \
	&& php -i \
	&& php -v

CMD ["php", "-v"]
