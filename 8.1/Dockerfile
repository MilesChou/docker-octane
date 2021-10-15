FROM php:8.1-rc

LABEL org.opencontainers.image.source="https://github.com/MilesChou/docker-octane" \
    repository="https://github.com/MilesChou/docker-octane" \
    maintainer="MilesChou <jangconan@gmail.com>"

# Set build deps
ENV BUILD_DEPS \
        libpq-dev \
        libsqlite3-dev

# See https://laravel.com/docs/8.x/deployment#server-requirements
# See https://pecl.php.net/package/swoole
RUN set -xe && \
            apt-get update && \
            apt-get install --yes --no-install-recommends --no-install-suggests \
                libpq5 \
                ${BUILD_DEPS} \
        && \
            docker-php-ext-install \
                pcntl \
                pdo_mysql \
                pdo_pgsql \
                pdo_sqlite \
        && \
            pecl install \
                swoole \
        && \
            docker-php-ext-enable \
                swoole \
        && \
            apt-get remove --purge -y ${BUILD_DEPS} && \
            apt-get autoremove --purge -y && \
            rm -r /var/lib/apt/lists/* && \
            php -m
