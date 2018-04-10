# PHP com suporte a Sybase e MS SQL

Dockerfile para a construção de imagem PHP com suporte a Sybase/MSSQL e dependências para desenvolvimento com Laravel ou Symfony.

## Requisitos
- [Docker CE](https://www.docker.com/community-edition#/download)

## Como usar a imagem
- docker pull uspdev/php-sybase:0.8
- docker run --rm -v ~/replicado:/usr/src/replicado -w /usr/src/replicado uspdev/php-sybase:0.8 php index.php
  - O comando acima é apenas um exemplo de uso

## Dockerfile

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
  php-zip\
  nodejs\
  composer

USER uspdev

CMD /bin/bash
```
