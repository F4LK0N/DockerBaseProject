FROM php:7.2-fpm-alpine

ENV PHALCON_VERSION=3.4.2
ENV XDEBUG_INI_FILE=/usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so php

# - apk add
#    para conseguir usar a funcao iconv (usada na impressao da avaliacao),
#    foi necessario incluir gnu-libiconv

RUN apk add --update make gcc g++ \
    libc-dev \
    autoconf \
    freetype-dev \
    libjpeg-turbo-dev \
    libpng-dev \
    libmcrypt-dev \
    libpcre32 \
    bzip2 \
    libbz2 \
    bzip2-dev \
    libmemcached-dev \
    cyrus-sasl-dev \
    binutils \
    libxml2-dev \
    icu-dev \
    zlib-dev \
    linux-headers \
    --repository http://dl-cdn.alpinelinux.org/alpine/edge/community/ \
    gnu-libiconv \
    && rm -rf /var/cache/apk/*

# - copy composer executable
COPY --from=composer /usr/bin/composer /usr/bin/

# - compile phalcon
RUN set -xe \
    && curl -LO https://github.com/phalcon/cphalcon/archive/v${PHALCON_VERSION}.tar.gz \
    && tar xzf v${PHALCON_VERSION}.tar.gz \
    && cd cphalcon-${PHALCON_VERSION}/build \
    && sh install \
    && cd ../.. \
    && rm -rf v${PHALCON_VERSION}.tar.gz cphalcon-${PHALCON_VERSION}

# - docker-php-ext-install
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd \
    && docker-php-ext-install mysqli \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install zip \
    && docker-php-ext-install pdo \
    && docker-php-ext-install pdo_mysql \
    && docker-php-ext-install opcache \
    && docker-php-ext-install soap \
    && docker-php-ext-install intl \
    && docker-php-ext-install exif \
    && docker-php-ext-install bcmath

# - pecl install
RUN pecl install -o -f redis-4.2.0 \
    && pecl install -o -f xdebug-2.7.0 \
    && pecl install -o -f mongodb-1.5.3 \
    && pecl install -o -f igbinary-3.0.0

RUN pecl install -f grpc

# - enable extensions
RUN docker-php-ext-enable redis mongodb igbinary phalcon xdebug grpc

# - php.ini files and configurations
#     variables_order.ini - para corrigir problema com filter_input, se a variavel estiver como EGPCS,
#     sempre é retornado null em operações semelhantes a: filter_input(INPUT_SERVER, 'HTTP_HOST')

RUN echo "xdebug.remote_port=10001" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.coverage_enable=0" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_enable=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_connect_back=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_log=/tmp/xdebug.log" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_autostart=true" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.remote_host=host.docker.internal" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.profiler_enable=1" >> ${XDEBUG_INI_FILE} \
    && echo "xdebug.profiler_output_dir=\"/var/www/html/profiler\"" >> ${XDEBUG_INI_FILE} \
    && echo "variables_order=GPCS" >> /usr/local/etc/php/conf.d/variables_order.ini
