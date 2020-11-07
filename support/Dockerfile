FROM wordpress:latest
RUN apt-get update
RUN apt-get install -y git
RUN php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');"
RUN cd /tmp/ && php composer-setup.php
RUN php -r "unlink('/tmp/composer-setup.php');"
RUN mv /tmp/composer.phar /usr/local/bin/composer
COPY composer.json /var/www/html/
ADD .vscode /var/www/html/.vscode
RUN composer install