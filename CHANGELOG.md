# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.4.1] - 2020-01-05
### Added
- Added libsodium to php 7.1 image.

### Changed
- Upgraded libsodium library to version 1.0.18.

## [1.4.0] - 2019-09-26
### Added
 - Added elasticsearch image

## [1.3.0] - 2019-08-17
### Added
- Added libsodium to php:7.2-fpm. [issue](https://github.com/ModestCoders/magento2-dockergento/issues/52)
- Added pcntl extension for concurrent job builds. (PR #8 by @ihor-sviziev)

### Changed
- Removed mysql client and added mariadb client on images php:7.1-fpm and php7.2-fpm
- Clean php:7.2-fpm images (PR #10, PR #9 by by @ihor-sviziev)

## [1.2.1] - 2018-12-11
### Added
- Add nginx images with capability to customize configuration.

### Fixed
- Fix UNISON_USER already exists.
- Fix php 7.2 build error. Libs were removed too soon.
- Fix permissions adding entypoint scripts.

## [1.2.0] - 2018-09-22
### Added
- Add node8-php7.2 image

## [1.1.0] - 1018-08-29
## Added
- Add image php:7.0-fpm
- Add image php:7.1-fpm
- Add image php:7.2-fpm

### Changed
- Avoid keeping alive node images.
- Avoid keeping alive unison containers.
### Fixed
- Add xdebug.remote_enable option.
- Fixed some documentation errors.
- Fixed permissions por user `app`.
- Fixed paths from unison volumes.

## [1.0.0] - 1018-08-24
### Added
- Add image node8-php7.0
- Add image node8-php7.1
- Add image unison.