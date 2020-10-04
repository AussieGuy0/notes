# Docker
A container is simply a running process, with encapsulation added to isolate it
from the host/other containers. A Docker Image includes everything needed to run
an application, including code/binaries/dependencies/files.

## Image
An image is a 'blueprint' of how a docker container is built.

A docker image has a unique `IMAGE ID` (looks a bit like a git commit hash!).

Images also have a `tag`, which specifies the version or variant of the docker
image. An example of this is the [postgres](https://hub.docker.com/_/postgres)
image, which provides different versions of postgres through tags. By default,
if a tag is not specified when pulling image, it will pull the image with the
`latest` tag.

### Base Image
An image can be based off an existing image using the `from` directive. This
utilises this existing image's functionality and extends it. For instance, if we
want to run our container in Ubuntu, we can do the following at the start of the
dockerfile:

```
FROM ubuntu:20.04
```

A base image is an image that sets it's `from` directive to `scratch`. Often
these are OS or language images such as `ubuntu` and `python`.

## Commands
### Pull
Pulls an image from a registry and saves it to the system.

### Run
Takes the supplied image and starts a new container (process) with it. 

It allows a command to be provided that will run in the container. For instance, if
we wanted to simply print "Hello World" using
[BusyBox](https://en.wikipedia.org/wiki/BusyBox), we can do the following:

`docker run busybox echo "Hello world"`

We can also spin up a container, then attach a terminal to it. We can do this
via providing the following arguments: `-it` (or `--interactive --tty`) and
running the `sh` command. Example:

`docker run -it busybox sh`

### Container
(All commands are prefixed with `docker container`)

- `prune` will remove all stopped containers

### port
List the port mappings of a specific container

```
$ docker port my-site
80/tcp -> 0.0.0.0:32722
```
The following can be read as: The port 80 of the docker container is mapped to
the host's port 32722. In this case, this would be accessible via
http://localhost:32722.

## Links
- https://docs.docker.com/
- https://docker-curriculum.com/
