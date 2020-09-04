FROM node:12

RUN apt-get update -y
RUN npm install -g grunt-cli && npm install -g bower

RUN apt-get install -y apt-transport-https lsb-release ca-certificates && \
    wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg && \
    echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list

RUN apt-get update && \
    apt-get install -y \
        php7.2 \
        php7.2-bcmath \
        php7.2-gd \
        php7.2-intl \
        php7.2-mbstring \
        php7.2-opcache \
        php7.2-pdo \
        php7.2-soap \
        php7.2-xsl \
        php7.2-zip \
        php7.2-pdo-mysql \
    && apt-get clean

RUN mkdir -p /home/app \
    && usermod -d /home/app -l app node \
    && chown -R app /home/app

USER app

WORKDIR /var/www/html
