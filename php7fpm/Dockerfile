FROM php:7.3-fpm

MAINTAINER Vitor Costa <vitor@tryideas.com.br>

ENV URL_SITE=http://localhost/

RUN apt-get update -y \
	&& apt-cache search pcre \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
	git \
	redis-tools \
	mariadb-client \
	nano \
	wget \
	tar \
	cron \
	curl \
	unzip \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -yqq \
	libxml2-dev \
	libfreetype6-dev \
	libicu-dev \
  	libssl-dev \
	libjpeg62-turbo-dev \
	libmcrypt-dev \
	libedit-dev \
	libedit2 \
	libxslt1-dev \
	libzip-dev \
	&& apt-get clean

# configure extensions
RUN docker-php-ext-configure \
  	gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/; \
  	docker-php-ext-install \
  	opcache \
  	gd \
  	bcmath \
  	intl \
  	mbstring \
  	pdo_mysql \
  	soap \
  	xsl \
  	zip
	  
RUN pecl install -o -f redis \
&&  rm -rf /tmp/pear \
&&  docker-php-ext-enable redis

RUN apt-get update \
  	&& apt-get install libpcre3 libpcre3 libpcre3-dev -yqq \
  	# php-pear \
  	&& pecl install oauth \
	&& echo "extension=oauth.so" > /usr/local/etc/php/conf.d/docker-php-ext-oauth.ini

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


# Install Mhsendmail
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install golang-go \
   && mkdir /opt/go \
   && export GOPATH=/opt/go \
   && go get github.com/mailhog/mhsendmail

COPY config/php.ini /usr/local/etc/php/php.ini

RUN chmod 777 -Rf /var/www /var/www/.* \
	&& chown -Rf www-data:www-data /var/www /var/www/.* \
	&& usermod -u 1000 www-data \
	&& chsh -s /bin/bash www-data

VOLUME /var/www/html
WORKDIR /var/www/html

EXPOSE 9000
CMD ["php-fpm"]
