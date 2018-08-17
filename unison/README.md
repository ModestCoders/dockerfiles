# Versions

`2.51.2` [(Dockerfile)](https://github.com/ModestCoders/dockerfiles/blob/master/unison/2.51.2/Dockerfile)

# Description
Bidirectional sync between container volumes and host without the performance compromises.

2 Types of sync:

* One time sync
* Continuosly watch and sync

# Motivation
In order to solve performance issues of directories bind-mounted with osxfs, you need to use docker volumes for large directories. Volumes however are not sync between container and host. There is where this image comes in handy. It allows you to bidirectionally sync volumes and host without affecting performance.

# Usage

### Docker-compose.yml
```
unison:
    image: modestcoders/unison:2.51.2
    volumes:
      - app-vendor:/var/www/html/magento/vendor
      - .vendor:/sync/vendor
      - ./magento/generated:/sync/magento/generated
    environment:
      - SYNC_SOURCE_BASE_PATH=/sync
      - SYNC_DESTINATION_BASE_PATH=/var/www/html
      - SYNC_MAX_INOTIFY_WATCHES=60000
    privileged: true

volumes:
  app-vendor:
```

### Commands

* One time sync

	```
	docker-compose unison sync -path <path_to_sync>
	```

* Continuosly sync

	```
	docker-compose unison watch -path <path_to_sync>
	```

# Environment Variables

You can configure the following variables in your `docker-compose.yml`

* `UNISON_USER`
* `UNISON_GROUP`
* `UNISON_UID`
* `UNISON_GID`
* `HOME`
* `SYNC_SOURCE_BASE_PATH`
* `SYNC_DESTINATION_BASE_PATH`
* `SYNC_PREFER`
* `SYNC_SILENT`
* `SYNC_MAX_INOTIFY_WATCHES`
* `SYNC_EXTRA_UNISON_PROFILE_OPTS`
* `SYNC_NODELETE_SOURCE`