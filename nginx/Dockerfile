
FROM debian:jessie

MAINTAINER Vitor Costa <vitor@tryideas.com.br>

RUN apt-get update -y \
	&& apt-cache search pcre \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends  \
    nginx \
    curl  \
    git   \
    nano  


RUN usermod -u 1000 www-data


ADD config/web.conf /etc/nginx/conf.d/

RUN chmod 777 -Rf /var/www /var/www/.* \
	&& chown -Rf www-data:www-data /var/www /var/www/.* \
	&& usermod -u 1000 www-data \
	&& chsh -s /bin/bash www-data

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
EXPOSE 443