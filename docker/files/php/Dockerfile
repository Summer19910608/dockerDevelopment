FROM php:7.3-fpm
RUN docker-php-ext-install pdo pdo_mysql mysqli \

&& pecl install redis-4.2.0 \
&& pecl install swoole \
&& pecl install yaconf \
&& docker-php-ext-enable redis swoole yaconf

# composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer

# use aliyun composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/