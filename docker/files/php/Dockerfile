FROM centos:7.2.1511

RUN apt-get update && apt-get install -y \
  libfreetype6-dev \
  libjpeg62-turbo-dev \
  libpng-dev \
&& docker-php-ext-install -j$(nproc) iconv \
&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
&& docker-php-ext-install -j$(nproc) gd \
&& docker-php-ext-configure pdo_mysql \
&& docker-php-ext-install pdo_mysql \
&& pecl install redis \
&& pecl install swoole \
&& pecl install yaconf \
&& docker-php-ext-enable redis swoole yaconf

# composer
RUN curl -sS https://getcomposer.org/installer | php \
    && mv composer.phar /usr/bin/composer

# use aliyun composer
RUN composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/