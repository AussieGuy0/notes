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

### Dockerfile


```docker
FROM node:14-alpine

WORKDIR /usr/src/app

# We copy the package.json first to utilise docker layer caching
COPY package*.json ./
RUN npm install
COPY . .

# What port the web app is listening on. The -p or -P command still has to be
# given when starting the container to publish the ports.
EXPOSE 4000

CMD ["npm", "start"]
```

#### A note about layers
A docker image is built up from a series of layers. Each instruction in a
Dockerfile produces a new layer. Each layer contains only the set a of
differences from the layer before it. It is important to note that the image
layers are read only!

When a container is created from an image, it adds a new writable layer on top
of the underlying image layers. This layer is referred to as the container
layer. Changes made during the running of the container affects only this
container layer.

As image layers are immutable, a single docker image can be shared across
multiple containers.

**Layer caching** occurs when docker can determine that a instruction does not
need to run, as a previous build has cached the layer. For instance, the `COPY`
instructions will not run if the external files being copied into the image have not
changed (via checksum). 

If **any** of the external files have changed, then the `COPY` instruction **and**
all subsequent instructions will be run.

It is useful to copy important, less changed files early on in the Dockerfile.
For instance, copying the `package.json` file and running `npm install` before
anything else means that Docker will be able to cache dependencies forever, as
long as the `package.json` file does not change.

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

We can expose the ports in a container (defined in a `Dockerfile`s `EXPOSE`) by
passing the -p or -P command. The lowercase -p allows explicit mapping of a
container's port to the host's port. For instance:

`docker run -p 8888:5000 web-app`

Exposes the container port 5000 to the host's port 8888.

The uppercase `-P` will expose all container ports (as defined by the
`EXPOSE` instructions in the `Dockerfile`) to random available ports on the
host.

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

## TODO
- Learn about volumes https://docs.docker.com/storage/volumes/
- Understand docker networking https://docs.docker.com/network/
