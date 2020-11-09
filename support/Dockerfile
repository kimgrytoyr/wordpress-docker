FROM composer:latest AS builder
WORKDIR /build
COPY composer.json .
RUN composer install

FROM wordpress:latest
RUN apt-get update
RUN apt-get install -y git vim
COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer
COPY composer.json /var/www/html/
ADD .vscode /var/www/html/.vscode
ENV NVM_DIR /root/.nvm
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | bash
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install 14.15"
COPY --from=builder /build/vendor /var/www/html/vendor
RUN mkdir /usr/local/etc/php/xdebug
RUN pecl install -f xdebug \
    && echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" > /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.coverage_enable=false" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.default_enable=1" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.remote_enable=1" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.remote_host=host.docker.internal" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.remote_port=9000" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.idekey=VSCODE" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.remote_autostart=false" >> /usr/local/etc/php/xdebug/xdebug.ini \
    && echo "xdebug.remote_enable=0" >> /usr/local/etc/php/php-cli.ini \
    && echo "export PHP_INI_SCAN_DIR=/usr/local/etc/php/conf.d:/usr/local/etc/php/xdebug" >> /etc/apache2/envvars
RUN echo "alias wp='wp --allow-root'" >> /root/.bashrc