FROM php8.5-apache

# packages
RUN sed -i 's|main|main non-free|' /etc/apt/sources.list.d/debian.sources && apt-get update && apt-get install -y \
    unixodbc \
    unixodbc-dev \
    freetds-bin \
    freetds-dev \
    libicu-dev \
    git \
    unzip \
    libzip-dev \
    libpng-dev \
    libonig-dev \
    libxml2-dev \
    libjpeg-dev \
    libfreetype6-dev \
    curl \
    memcached

# cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

# composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# php libs
RUN docker-php-ext-install \
    intl \
    pdo_mysql \
    mysqli \
    soap \
    zip \
    mbstring \
    bcmath \
    pdo_dblib \
    memcached

# gd
RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install gd

# php memory
ENV PHP_MEMORY_LIMIT=512M
ENV PHP_UPLOAD_LIMIT=512M

RUN { \
        echo "memory_limit=${PHP_MEMORY_LIMIT}"; \
        echo "upload_max_filesize=${PHP_UPLOAD_LIMIT}"; \
        echo "post_max_size=${PHP_UPLOAD_LIMIT}"; \
    } > "${PHP_INI_DIR}/conf.d/upload.ini"

# memcached de acordo com uspdev/cache
ENV MEMCACHED=5M

# atualizar ou adicionar a configuração
RUN grep -qE "^I" /etc/memcached.conf \
    && sed -i "s/^I.*/I = ${MEMCACHED}/" /etc/memcached.conf \
    || echo "I = ${MEMCACHED}" >> /etc/memcached.conf

# apache
RUN a2enmod rewrite

RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
