FROM php:8.3-fpm
RUN apt-get update && apt-get install -y \
		libfreetype-dev \
		libjpeg62-turbo-dev \
		libpng-dev \
        libcurl3-dev \
        libcurl4-openssl-dev \
        #xml
        libxml2-dev \
        #mbstring
        libonig-dev \
        #imap
        libkrb5-dev \
        libc-client-dev \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd

RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql

RUN docker-php-ext-install bcmath
RUN docker-php-ext-install curl
#RUN docker-php-ext-install dev
RUN docker-php-ext-configure imap --with-kerberos --with-imap-ssl && docker-php-ext-install imap

RUN docker-php-ext-install intl
RUN docker-php-ext-install mbstring

RUN docker-php-ext-install xml

RUN sed -i 's/listen = /;listen = /' /usr/local/etc/php-fpm.d/www.conf

WORKDIR /

CMD ["php-fpm"]
