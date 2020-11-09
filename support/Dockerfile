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
ENV NVM_DIR /root/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install 14.15"
COPY --from=builder /build/vendor /var/www/html/vendor
RUN pecl install -f xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/conf.d/xdebug.ini;
EXPOSE 9000