# Docker-owncloud

[OwnCloud](http://owncloud.org/) images for Docker.
For use with [Docker](http://docker.io)

All suggestions and contributions are very welcome.
There is a room for tons of improvements, so please feel free to open issues and pull requests to help improve these images.


## Getting stared

### Requirements
 * [Git](http://git-scm.com/)
 * [Docker](http://docker.io)

### Get the source code
```
  $ git clone git@github.com:spiroid/docker-owncloud.git
  $ cd docker-owncloud
```

## Intro

This builds two docker elements in order to run owncloud :

* One image with a nginx + php-fpm web server with configuration options tuned for owncloud
* A docker data container volume in order to allow you to persist the data between different containers


## Postgresql database

The default install is setup for PostgreSQL database, but no docker image is provided.
Please use an already existing and well prepared postgresql image from docker hub, or use fig :)
More on that in the next section.


## Build

### FIG


### Building manually

Replace ```<your pseudo>``` by a prefix you want to appear in your local docker image registry.

```
$ docker build -t <your pseudo>/owncloud ./owncloud
$ docker build -t <your pseudo>/owncloud-nginx ./owncloud-nginx
```


## Running with fig

As simple as :

```
  $ fig up
```


## TODO

See [TODO](TODO.md) file for a short list.


## LICENSE

See [LICENSE](LICENSE) file.


## Resources

### Other Docker images
 * [Docker - NGINX - PHP5](https://github.com/darron/docker-nginx-php5)
 * [Docker - NGINX](https://github.com/orchardup/docker-nginx)
 * [Docker - NGINX - Supervisor](https://github.com/dz0ny/docker-wpdev)

### Blog articles
 * [Docker and OwnCloud - part 1](http://dischord.org/blog/2013/07/10/docker-and-owncloud/)
 * [Docker and OwnCloud - part 2](http://dischord.org/blog/2013/08/13/docker-and-owncloud-part-2/)

### Other
 * [Stackoverflow - running postgresql with supervisord](http://stackoverflow.com/questions/11092358/running-postgresql-with-supervisord)
