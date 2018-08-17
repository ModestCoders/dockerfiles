FROM alpine:3.6
MAINTAINER Juan Alonso <juan.jalogut@gmail.com>

# Alpine doesn't ship with Bash.
RUN apk add --no-cache bash

# Install Unison from source with inotify support + remove compilation tools
ARG UNISON_VERSION=2.51.2
RUN apk add --no-cache --virtual .build-dependencies build-base curl && \
    apk add --no-cache inotify-tools ocaml && \
    curl -L https://github.com/bcpierce00/unison/archive/v$UNISON_VERSION.tar.gz | tar zxv -C /tmp && \
    cd /tmp/unison-${UNISON_VERSION} && \
    sed -i -e 's/GLIBC_SUPPORT_INOTIFY 0/GLIBC_SUPPORT_INOTIFY 1/' src/fsmonitor/linux/inotify_stubs.c && \
    make UISTYLE=text NATIVE=true STATIC=true && \
    cp src/unison src/unison-fsmonitor /usr/local/bin && \
    apk del .build-dependencies ocaml && \
    rm -rf /tmp/unison-${UNISON_VERSION}

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

COPY scripts/sync.sh /usr/local/bin/sync
COPY scripts/watch.sh /usr/local/bin/watch

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["tail", "-f", "/dev/null"]