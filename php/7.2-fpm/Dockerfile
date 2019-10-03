FROM php:7.2-fpm
MAINTAINER Juan Alonso <juan.jalogut@gmail.com>

RUN apt-get update && apt-get install -y \
  cron \
  git \
  gzip \
  libfreetype6-dev \
  libicu-dev \
  libjpeg62-turbo-dev \
  libmcrypt-dev \
  libpng-dev \
  libxslt1-dev \
  lsof \
  mariadb-client \
  vim \
  zip \
  procps \
  sudo \
  wget \
  && rm -rf /var/lib/apt/lists/*

RUN wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
RUN tar xvzf LATEST.tar.gz
RUN cd libsodium-stable && \
    ./configure && \
    make && make check && \
    make install

RUN docker-php-ext-configure \
  gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/

RUN docker-php-ext-install \
  bcmath \
  gd \
  intl \
  mbstring \
  opcache \
  pcntl \
  pdo_mysql \
  soap \
  xsl \
  zip \
  sodium

RUN docker-php-ext-enable sodium

RUN pecl channel-update pecl.php.net \
  && pecl install xdebug \
  && docker-php-ext-enable xdebug \
  && sed -i -e 's/^zend_extension/\;zend_extension/g' /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Clean up apt-get update
RUN rm -rf /var/lib/apt/lists/*

RUN curl -sS https://getcomposer.org/installer | \
  php -- --install-dir=/usr/local/bin --filename=composer

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app

COPY conf/www.conf /usr/local/etc/php-fpm.d/
COPY conf/php.ini /usr/local/etc/php/
COPY conf/xdebug.ini /usr/local/etc/php/conf.d/
COPY conf/php-fpm.conf /usr/local/etc/

RUN mkdir /sock
RUN chown -R app:app /usr/local/etc/php/conf.d /sock

RUN mkdir -p /var/www && chown -R app:app /var/www/
RUN echo "app ALL=(ALL) NOPASSWD: /bin/chown" >> /etc/sudoers.d/app

USER app:app

VOLUME /var/www

WORKDIR /var/www/html

EXPOSE 9001

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "php-fpm" ]
