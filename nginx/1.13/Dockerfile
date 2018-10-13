FROM nginx:1.13
MAINTAINER Juan Alonso <juan.jalogut@gmail.com>

RUN apt-get update \
	&& apt-get install -y sudo \
	&& rm -rf /var/lib/apt/lists/*

RUN groupadd -g 1000 app \
 && useradd -g 1000 -u 1000 -d /var/www -s /bin/bash app
RUN touch /var/run/nginx.pid
RUN mkdir /sock
RUN chown -R app:app /var/cache/nginx/ /var/run/nginx.pid /sock

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/default.conf /etc/nginx/conf.d/

RUN echo "app ALL=(ALL) NOPASSWD: /bin/cp -f /var/www/conf/nginx/default.conf /etc/nginx/conf.d/" >> /etc/sudoers.d/app

USER app:app

VOLUME /var/www

WORKDIR /var/www/html

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT [ "docker-entrypoint.sh" ]
CMD [ "nginx", "-g", "daemon off;" ]