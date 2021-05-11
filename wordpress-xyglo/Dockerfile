FROM wordpress:5.7.1-php7.4-apache

COPY ./htaccess-additions.txt htaccess-additions.txt
RUN cat htaccess-additions.txt >> /var/www/html/.htaccess

#/usr/local/bin/bash: :q: command not found
#RUN cat ./php-additions.ini >> /usr/local/etc/php/php.ini
#COPY ./uploads.ini /usr/local/etc/php/conf.d/uploads.ini

