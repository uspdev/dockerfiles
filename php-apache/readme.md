Dockerfile para imagens a partir de php-apache, com dependências usadas na USP, como soap e sybase.

https://hub.docker.com/r/uspdev/uspdev-php-apache

Usando no seu sistema em Laravel:

    FROM uspdev/uspdev-php-apache:latest

    RUN sed -i 's|/var/www/html|/var/www/html/public|' \
        /etc/apache2/sites-available/000-default.conf

    USER www-data

    COPY --chown=www-data . .

    RUN composer install \
        --no-dev \
        --optimize-autoloader \
        --no-interaction

    CMD ["apache2-foreground"]

Usando no seu sistema em Drupal:

    FROM uspdev/uspdev-php-apache:latest

    RUN sed -i 's|/var/www/html|/var/www/html/web|' /etc/apache2/sites-available/000-default.conf

    # composer
    USER www-data
    COPY --chown=www-data . .
    RUN composer install

    CMD ["apache2-foreground"]

