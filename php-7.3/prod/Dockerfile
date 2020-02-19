FROM alpine:3.11

WORKDIR /var/www/html

# Install common packages
RUN apk add --no-cache --update \
    curl

# Install PHP extensions
RUN apk add --no-cache --update \
    php7 \
    php7-ctype \
    php7-dom \
    php7-iconv \
    php7-intl \
    php7-json \
    php7-mbstring \
    php7-opcache \
    php7-pdo_mysql \
    php7-posix \
    php7-session \
    php7-simplexml \
    php7-tokenizer \
    php7-xml

# Install Nginx Unit
RUN apk add --no-cache --update \
    unit \
    unit-php7

# Copy Nginx Unit configuration file to image
COPY ./nginx-unit-config.json /etc/unitd/conf.d/config.json

# Copy entrypoint shell to image
COPY ./entrypoint /usr/local/bin/

# Copy PHP "hello world" script to image
COPY ./index.php /var/www/html/public/index.php

HEALTHCHECK --interval=15s --timeout=5s CMD curl --fail --user-agent 'docker/health-check' http://localhost:8080/ || exit 1

EXPOSE 8080

CMD ["entrypoint"]
