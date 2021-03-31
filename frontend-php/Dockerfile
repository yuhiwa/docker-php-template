FROM php:7.3-fpm-buster

RUN rm /etc/localtime \
    && echo "Asia/Tokyo" > /etc/timezone \
    && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
        libicu-dev git unzip \
    && docker-php-ext-install -j$(nproc) iconv intl mbstring pdo_mysql opcache bcmath zip \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN curl -L -o /tmp/wkhtmltox.deb https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && apt-get -qy install /tmp/wkhtmltox.deb

# font install 
RUN curl -L -o  /tmp/IPAexfont00201.zip https://moji.or.jp/wp-content/ipafont/IPAexfont/ipaexg00201.zip \
    && unzip /tmp/IPAexfont00201.zip \
    && mv ipaexg00201 /usr/share/fonts/ && rm /tmp/IPAexfont00201.zip

COPY php.ini /usr/local/etc/php/
COPY ./php-fpm.d/www.conf /usr/local/etc/php-fpm.d/www.conf

# install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN pecl install xdebug-2.8.0 && docker-php-ext-enable xdebug
COPY xdebug.ini /usr/local/etc/php/conf.d/
