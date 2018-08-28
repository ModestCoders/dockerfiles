FROM node:8

RUN apt-get update -y
RUN npm install -g grunt-cli && npm install -g bower

RUN apt-get install -y apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && \
    apt-get install -y \
        php7.0 \
        php7.0-bcmath \
        php7.0-gd \
        php7.0-intl \
        php7.0-mbstring \
        php7.0-mcrypt \
        php7.0-opcache \
        php7.0-pdo \
        php7.0-soap \
        php7.0-xsl \
        php7.0-zip \
        php7.0-pdo-mysql \
    && apt-get clean

RUN mkdir -p /home/app \
    && usermod -d /home/app -l app node \
    && chown -R app /home/app

USER app

WORKDIR /var/www/html