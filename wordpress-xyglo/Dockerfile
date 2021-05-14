FROM wordpress:5.7.1-php7.4-apache

RUN touch /usr/local/etc/php/conf.d/uploads.ini \
    && echo "file_uploads = On;\n\
             memory_limit = 500M;\n\
             upload_max_filesize = 100M;\n\
             post_max_size = 100M;\n\
             max_execution_time = 180M;" >> /usr/local/etc/php/conf.d/uploads.ini

RUN touch /var/www/html/.htaccess \
    && echo "php_value post_max_size 24M\n\
             php_value upload_max_filesize 80M" >> /var/www/html/.htaccess

COPY network.php /usr/src/wordpress/wp-admin/includes/network.php
COPY ./htaccess.txt /var/www/html/.htaccess

#RUN cat ./php-additions.ini >> /usr/local/etc/php/php.ini
#COPY ./uploads.ini /usr/local/etc/php/conf.d/uploads.ini

