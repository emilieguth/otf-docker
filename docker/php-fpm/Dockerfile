FROM php:8.4-fpm
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
        libyaml-dev \
        bash \
        vim \
	&& docker-php-ext-configure gd --with-freetype --with-jpeg \
	&& docker-php-ext-install -j$(nproc) gd \
    && docker-php-ext-install exif

RUN ln -sf /bin/bash /bin/sh

RUN pecl install -o -f redis \
    &&  rm -rf /tmp/pear \
    &&  docker-php-ext-enable redis

RUN pecl install yamL \
    && docker-php-ext-enable yaml

RUN apt-get update -yqq \
    && apt-get install -y libmagickwand-dev imagemagick

RUN docker-php-ext-install mysqli pdo pdo_mysql && docker-php-ext-enable pdo_mysql
RUN pecl install imap && \
    docker-php-ext-enable imap
RUN docker-php-ext-install curl


# Workaround for imagick
RUN curl -L -o /tmp/imagick.tar.gz https://github.com/Imagick/imagick/archive/7088edc353f53c4bc644573a79cdcd67a726ae16.tar.gz \
&& tar --strip-components=1 -xf /tmp/imagick.tar.gz \
&& phpize \
&& ./configure \
&& make \
&& make install \
&& echo "extension=imagick.so" > /usr/local/etc/php/conf.d/ext-imagick.ini \
&& rm -rf /tmp/*

# Should add imagick with these command lines :
#RUN pecl install -o -f imagick
#RUN docker-php-ext-enable imagick

#RUN docker-php-ext-install dev # Passage à PHP 8.4 ?

RUN docker-php-ext-install intl
RUN docker-php-ext-install mbstring

RUN docker-php-ext-install xml

RUN sed -i 's/listen = /;listen = /' /usr/local/etc/php-fpm.d/www.conf


WORKDIR /

CMD ["php-fpm"]
