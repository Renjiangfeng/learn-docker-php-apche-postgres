FROM php:5.5.25-apache

ADD apt-list /opt/

# use 163 sources to boost
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak \ 
	&& cat /opt/apt-list >/etc/apt/sources.list \ 
	&& apt-get update && \
    apt-get install -y libmcrypt-dev libpq-dev && \
    docker-php-ext-configure pgsql -with-pgsql=/usr/local/pgsql && \
    docker-php-ext-install mcrypt pdo_mysql pdo_pgsql mbstring

# add yac module
COPY extension/yac.so /usr/local/lib/php/extensions/no-debug-non-zts-20151012
COPY extension/yac.ini  /usr/local/etc/php/conf.d
COPY php.ini  /usr/local/etc/php/

WORKDIR /www

# restart php-fpm
#RUN kill -USR2 1