# Dokku

## Install

### install dokku
https://github.com/dokku/dokku

$ wget https://raw.githubusercontent.com/dokku/dokku/v0.14.6/bootstrap.sh
$ sudo DOKKU_TAG=v0.14.6 bash bootstrap.sh

### redis
https://github.com/dokku/dokku-redis

$ sudo dokku plugin:install https://github.com/dokku/dokku-redis.git redis

### lets encrypt
https://github.com/dokku/dokku-letsencrypt

$ sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git

## 실행

### 앱생성
dokku apps:create <app_name>
dokku config:set <app_name> ENVNAME=ENVVALUE

### redis 생성
dokku redis:create <redis_name>
dokku redis:link <redis_name> <app_name>

### https letsencrypt
dokku letsencrypt <app_name>


