# PHP com suporte a Sybase e MS SQL

Dockerfile para a construção de imagem PHP com suporte a Sybase/MSSQL e dependências para desenvolvimento com Laravel ou Symfony.

```
FROM debian:testing

MAINTAINER USPdev devs@usp.br uspdev.github.io

LABEL Description="Image for PHP 7.2 development with Sybase and MS-SQL support."

RUN useradd -ms /bin/bash uspdev &&\
  apt-get update &&\
  apt-get install -y\
  php-cli\
  php-bcmath\
  php-xml\
  php-mbstring\
  php-mysql\
  php-sybase\
  nodejs\
  composer

USER uspdev

WORKDIR /home/uspdev

CMD /bin/bash
```
