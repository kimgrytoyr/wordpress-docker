FROM composer:latest AS builder
WORKDIR /build
COPY composer.json .
RUN composer install

FROM wordpress:latest
RUN apt-get update
RUN apt-get install -y git
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
COPY composer.json /var/www/html/
ADD .vscode /var/www/html/.vscode
RUN composer install