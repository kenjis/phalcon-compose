<img align="right" width="175px" src="http://i.imgur.com/mdZ8Ktf.png" />

# Phalcon 2.1 Docker Edition [![Build Status](https://travis-ci.org/sergeyklay/phalcon-compose.svg?branch=master)](https://travis-ci.org/sergeyklay/phalcon-compose) [![phalcon-2.1.x](https://img.shields.io/badge/phalcon-2.1.x-blue.svg)](https://github.com/sergeyklay)

The *unofficial* Phalcon Docker Edition – by [@sergeyklay](https://github.com/sergeyklay)

This is an unofficial, open-source and community-driven boilerplate for Phalcon projects that run on [Docker][0].
It's an attempt of standardizing and making it easier to bootstrap Phalcon applications ready for development and production environments.
The main tools used are Phalcon, Docker and Docker Compose. Other things included are:

- Nginx 1.9.11
- MySQL 5.7.11
- Memcached 1.4
- PHP 5.6.19 + PHP-FPM
- Xdebug 2.3.3
- Opcache 7.0.6-dev
- Beanstalk 1.10
- Redis 3.0.7
- Aerospike 3.7.4

## Get Started

### Dependencies

To run this stack on your machine, you need at least:

* Operating System: Windows, Linux, or OSX
* [Docker Engine][1] >= 1.10
* [Docker Compose][2] >= 1.6.2

### Installation

First, clone this repository:

```sh
$ git clone git@github.com:sergeyklay/phalcon-compose.git
```

Next, put your Phalcon application into `application` folder.
Then add `your_site_name.dev` in your `/etc/hosts` file as follows:

```
127.0.0.1	your_site_name.dev
```

## Usage

Now you are ready to build, creates, start, and attach to containers for your application, run:

```sh
docker-compose -p phalcon up -d
```

and you can visit your Phalcon application on the following URL: http://your_site_name.dev

### Containers Included

Here are the `docker-compose` services:

```
 application         Phalcon 2.1.x application code container
 mysql               MySQL 5.7.11 database container
 redis               Redis 3.0 database container
 memcached           Memcached Server 1.4 container
 queue               Beanstalk 1.10 queue container
 php                 PHP 5.6.19 + PHP-FPM container in which the application volume is mounted
 nginx               Nginx 1.9.11 webserver container in which application volume is mounted too
 aerospike           The Aerospike Server 3.7.4
```

This results in the following running containers:

```sh
$ docker-compose -p phalcon ps

       Name                     Command              State                                               Ports
-----------------------------------------------------------------------------------------------------------------------------------------------------------
phalcon_aerospike     /entrypoint.sh asd             Up      0.0.0.0:3000->3000/tcp, 0.0.0.0:3001->3001/tcp, 0.0.0.0:3002->3002/tcp, 0.0.0.0:3003->3003/tcp
phalcon_beanstalkd    beanstalkd -p 11300 -b /data   Up      0.0.0.0:11300->11300/tcp
phalcon_memcached     /entrypoint.sh memcached       Up      0.0.0.0:11211->11211/tcp
phalcon_mysql         /entrypoint.sh mysqld          Up      0.0.0.0:3306->3306/tcp
phalcon_nginx         nginx -g daemon off;           Up      0.0.0.0:443->443/tcp, 0.0.0.0:80->80/tcp
phalcon_php_5.6_fpm   php5-fpm -F                    Up      0.0.0.0:10000->10000/tcp, 0.0.0.0:9000->9000/tcp
phalcon_redis         /entrypoint.sh redis-server    Up      0.0.0.0:6379->6379/tcp
phalcon_volume        /bin/bash                      Up

```

### Read logs

You can access logs by using `docker logs <container_name>` into your host machine.

[0]: https://www.docker.com/
[1]: https://docs.docker.com/installation/
[2]: https://docs.docker.com/compose/install/
