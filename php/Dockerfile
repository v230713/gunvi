# docker/php/Dockerfile

FROM php:7.1.11-fpm-alpine
#VOLUME ["./public_html","/public_html"]
RUN curl https://getcomposer.org/composer.phar > /usr/local/bin/composer \
    && chmod a+x /usr/local/bin/composer

# customized ini directives for my app
#COPY conf.d/php-fpm.conf /usr/local/etc/php/conf.d/app.ini
RUN apk add --no-cache \
             libmcrypt-dev \
             libltdl \
       && docker-php-ext-configure mcrypt \
       && docker-php-ext-install mcrypt 

RUN apk add --no-cache freetype libpng libjpeg-turbo freetype-dev libpng-dev libjpeg-turbo-dev && \
docker-php-ext-configure gd \
--with-gd \
--with-freetype-dir=/usr/include/ \
--with-png-dir=/usr/include/ \
--with-jpeg-dir=/usr/include/ && \
NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) && \
docker-php-ext-install -j${NPROC} gd && \
apk del --no-cache freetype-dev libpng-dev libjpeg-turbo-dev
RUN apk update
RUN apk add git
RUN docker-php-ext-install pdo pdo_mysql
RUN mkdir /public_html
WORKDIR /public_html
COPY ./public_html /public_html
RUN ls -ltr /public_html
# install deps
#RUN composer require onelogin/php-saml:"dev-remove_mcrypt as 2.11.0"
RUN composer install

