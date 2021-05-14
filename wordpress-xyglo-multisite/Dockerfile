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

RUN touch /var/www/html/wp-config.php \
    && echo "# Require SSL for admin and logins \
               define( 'FORCE_SSL_ADMIN', false ); \
               # Disable plugin and theme update and installation \
               define( 'DISALLOW_FILE_MODS', false ); \
               # Disable the plugin and theme editor \
               define( 'DISALLOW_FILE_EDIT', false ); \
               # Multisite \
               #define( 'WP_ALLOW_MULTISITE', true ); \
               #define( 'MULTISITE', true); \
               #define( 'SUBDOMAIN_INSTALL', false); \
               #define( 'DOMAIN_CURRENT_SITE', 'xyglo.com'); \
               #define( 'PATH_CURRENT_SITE', '/'); \
               #define( 'SITE_ID_CURRENT_SITE', 1); \
               #define( 'BLOG_ID_CURRENT_SITE', 1); \
               #define( 'WP_MEMORY_LIMIT', '256M' ); \
               #define( 'WP_MAX_MEMORY_LIMIT', '256M'); \
               set_time_limit (60);" >> /var/www/html/wp-config.php
