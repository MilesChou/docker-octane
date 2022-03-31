FROM php:8.0

LABEL org.opencontainers.image.source="https://github.com/MilesChou/docker-octane" \
    repository="https://github.com/MilesChou/docker-octane" \
    maintainer="MilesChou <jangconan@gmail.com>"

# Set build deps
ENV BUILD_DEPS \
        libpq-dev \
        libpq5 \
        libsqlite3-dev \
        rsyslog \
        libxml2-dev

# See https://laravel.com/docs/8.x/deployment#server-requirements
# See https://pecl.php.net/package/swoole
RUN set -xe && \
            apt-get update && \
            apt-get install --yes --no-install-recommends --no-install-suggests \
                ${BUILD_DEPS} \
        && \
            docker-php-ext-install \
                pcntl \
                pdo_mysql \
                pdo_pgsql \
                pdo_sqlite \
                soap \
        && \
            pecl install \
                mongodb-1.12.0 \
                redis-5.3.6 \
                swoole-4.8.6 \
        && \
            docker-php-ext-enable \
                mongodb \
                redis \
                swoole \
        && \
            apt-get remove --purge -y ${BUILD_DEPS} && \
            apt-get autoremove --purge -y && \
            rm -r /var/lib/apt/lists/* && \
            php -m
