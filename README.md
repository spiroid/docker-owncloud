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


## OwnCloud + NGINX + Postgresql

This docker image is based on [Debian Jessie](http://www.debian.org/releases/testing/) release and contains all the components with no external dependencies.
Installed applications:

* NGINX as front webserver
* Postgresql as database backend
* PHP5 + PHP-FPM
* OwnCloud version 6.0.0a
* Supervisord to monitor running processes


### Some details

#### SSL Certificate

Your owncloud instance will only be avaiable on HTTPS. In order to make it work you'll need to provide a valid SSL certificate. It can be a self signed certificate or a certificate generated and signed by a trusted authority.
You need to put a couple of files in the resources/ssl directory. The expected file names are owncloud.crt and owncloud.key and they are *required* to successfully generate the docker image.


#### Postgresql database

A specific postgresql database is created during the build process.
I followed vagrant conventions and by default the db name, user and password are 'owncloud'



### Building the image

cd to the directory where you cloned the repository.


```
  $ cd owncloud-postgresql
  $ docker build -t <your pseudo>/owncloud-postgresql .
```

replace ```<your pseudo>``` by a prefix you want to appear in your local docker image registry.


### Runnning the container

```
  $ docker run -p 443 -h 'hostname' -d  <your pseudo>/owncloud-postgresql
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
