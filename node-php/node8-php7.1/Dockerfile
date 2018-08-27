FROM node:8

RUN apt-get update -y
RUN npm install -g grunt-cli && npm install -g bower

RUN apt-get install -y apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && \
    apt-get install -y \
        php7.1 \
        php7.1-bcmath \
        php7.1-gd \
        php7.1-intl \
        php7.1-mbstring \
        php7.1-mcrypt \
        php7.1-opcache \
        php7.1-pdo \
        php7.1-soap \
        php7.1-xsl \
        php7.1-zip \
        php7.1-pdo-mysql \
    && apt-get clean

WORKDIR /var/www/html