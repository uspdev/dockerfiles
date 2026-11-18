# uspdev-php-apache

Imagens Docker que adicionam uma camada (layer) sobre as imagens oficiais do PHP com Apache
(`php:<versão>-apache`), incluindo dependências usadas na USP, como soap e sybase.

Docker Hub: https://hub.docker.com/r/uspdev/uspdev-php-apache

Versões disponíveis (uma pasta por versão do PHP) e a imagem oficial usada como base:

| Versão | Imagem base |
|--------|-------------|
| `8.3`  | [php:8.3-apache](https://hub.docker.com/layers/library/php/8.3-apache/) |
| `8.4`  | [php:8.4-apache](https://hub.docker.com/layers/library/php/8.4-apache/) |
| `8.5`  | [php:8.5-apache](https://hub.docker.com/layers/library/php/8.5-apache/) |

## Gerando a imagem localmente

Entre na pasta da versão desejada e faça o build:

    cd 8.3
    docker build -t uspdev/uspdev-php-apache:8.3 .

Teste a imagem gerada:

    docker run --rm uspdev/uspdev-php-apache:8.3 apache2 -v
    docker run --rm uspdev/uspdev-php-apache:8.3 php --version
    docker run --rm uspdev/uspdev-php-apache:8.3 php -m

Para forçar um build do zero (sem cache e baixando a imagem base mais recente):

    docker build --no-cache --pull -t uspdev/uspdev-php-apache:8.3 .

## Publicando no Docker Hub

1. Faça login com uma conta que tenha permissão de escrita na organização `uspdev`:

        docker login

2. Envie a tag da versão:

        docker push uspdev/uspdev-php-apache:8.3

3. Se essa for a versão mais recente, atualize também a tag `latest`:

        docker tag uspdev/uspdev-php-apache:8.3 uspdev/uspdev-php-apache:latest
        docker push uspdev/uspdev-php-apache:latest


## Usando no seu sistema em Laravel

    FROM uspdev/uspdev-php-apache:8.3

    RUN sed -i 's|/var/www/html|/var/www/html/public|' \
        /etc/apache2/sites-available/000-default.conf

    USER www-data

    COPY --chown=www-data . .

    RUN composer install \
        --no-dev \
        --optimize-autoloader \
        --no-interaction

    CMD ["apache2-foreground"]

## Usando no seu sistema em Drupal

    FROM uspdev/uspdev-php-apache:8.3

    RUN sed -i 's|/var/www/html|/var/www/html/web|' /etc/apache2/sites-available/000-default.conf

    # composer
    USER www-data
    COPY --chown=www-data . .
    RUN composer install

    CMD ["apache2-foreground"]

Troque `8.3` pela versão desejada, ou use `latest`.
