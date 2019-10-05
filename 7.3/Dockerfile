FROM ubuntu:16.04
MAINTAINER shazi7804 <shazi7804@gmail.com>

ENV PHP_VERSION 7.3

# Add non-free and packages
RUN echo 'deb http://archive.ubuntu.com/ubuntu/ xenial multiverse \n\
deb http://archive.ubuntu.com/ubuntu/ xenial-updates multiverse \n\
deb http://archive.ubuntu.com/ubuntu/ xenial-backports main restricted universe multiverse' >> /etc/apt/sources.list

# Add php ppa
RUN set -ex \
      && apt-get update && apt-get install -y \
           python-software-properties \
           software-properties-common \
           language-pack-en-base \ 
      && export LC_ALL=en_US.UTF-8 \
      && export LANG=en_US.UTF-8 \
      && add-apt-repository ppa:ondrej/php

# Install package
RUN set -ex \
      && DEBIAN_FRONTEND=noninteractive \
      && apt-get update && apt-get install -y \
         curl \
         apache2 libapache2-mod-fcgid \
         php${PHP_VERSION}-cli \
         php${PHP_VERSION}-cgi \
         php${PHP_VERSION}-common \
         php${PHP_VERSION}-fpm \
         php${PHP_VERSION}-mysql \
         php${PHP_VERSION}-mongodb \
         php${PHP_VERSION}-gd \
         php${PHP_VERSION}-json \
         php${PHP_VERSION}-bcmath \
         php${PHP_VERSION}-mbstring \
         php${PHP_VERSION}-xml \
         php${PHP_VERSION}-xmlrpc \
         php${PHP_VERSION}-zip \
         php${PHP_VERSION}-soap \
         php${PHP_VERSION}-sqlite3 \
         php${PHP_VERSION}-curl \
         php${PHP_VERSION}-opcache \
         php${PHP_VERSION}-readline

# set apache module
RUN set -ex \
      && a2dismod mpm_event \
      && a2enmod fcgid mpm_worker actions rewrite

RUN echo "<IfModule mod_fcgid.c> \n\
  AddHandler fcgid-script .php \n\
  FcgidWrapper /usr/bin/php-wrapper .php \n\
  FcgidConnectTimeout 20 \n\
  <IfModule mod_mime.c> \n\
    AddHandler fcgid-script .php \n\
  </IfModule> \n\
</IfModule> \n\
" > /etc/apache2/mods-available/fcgid.conf

RUN echo "#!/bin/sh \n\
# Set desired PHP_FCGI_* environment variables. \n\
# Example: \n\
# PHP FastCGI processes exit after 500 requests by default. \n\
PHP_FCGI_MAX_REQUESTS=10000 \n\
export PHP_FCGI_MAX_REQUESTS \n\
\n\
# Replace with the path to your FastCGI-enabled PHP executable \n\
exec /usr/bin/php-cgi \n\
" > /usr/bin/php-wrapper \
    && chmod +x /usr/bin/php-wrapper

RUN sed -i 's/;date.timezone =.*/date.timezone = Asia\/Taipei/g' /etc/php/${PHP_VERSION}/cgi/php.ini

COPY /conf/vhost.conf /etc/apache2/sites-available/000-default.conf
COPY /index.php /var/www/html/

# Expose port 80 to the outside
EXPOSE 80

#COPY conf/supervisord.conf /etc/supervisor/conf.d/supervisord.conf
#CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]

COPY /scripts/start.sh /start.sh
CMD ["/start.sh"]
