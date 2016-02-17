# Docker tutorial
This tutorial can be considered as notes taken from Docker documentation and other learning using docker. It walks the reader trough and explains the main concepts of the docker.

**WORK IN PROGRESS** - This project is in early stage and is incomplete.

## Docker Architecture

### Docker images
Read only template. For example, it can be Ubuntu operation system with Apache and a web application installed. We use `docker build to build a new image. They are used to create a container.`
It is the `build` component of the docker.

### Docker container
Holds everything needed for application to run. Container is always created from docker image. It can be stop, start, moved, removed and deleted. 
Docker container is the `run` component of the docker.

### Docker registry
Stores and makes available docker images. If the docker image can not be found locally, it will be downloaded from the registry. Some of them are [docker hub](https://hub.docker.com/) and [quai](https://quay.io).

### Docker image
As was describe above, docker image is immutable template used for launching docker containers. Every image starts from a base image such as ubuntu. Further, using descriptive commands **instructions** to build the image. Each instruction creates a layer a new layer in the image. These instructions may be for example:

- Run a command
- Add a file or directory
- Create an environmental variable
- Define process to run when launching a container

**Dockerfile** stores above instructions and docker produces a docker image by executing them.

### Running docker container

`$ docker run -i -t ubuntu /bin/bash`

Runs `ubuntu` image with command `/bin/bash`

Under the hood docker:

- Pulls the `ubunt` image if it does not exists locally. By default, it tries to pull the image from [Docker Hub](https://hub.docker.com/).
- Creates a container
- Allocates a filesystem and mounts a read-write layer
- Allocates a network / bridge interface - to communicate with localhost
- Sets up an IP address
- Run predefined operation
- Captures STDOUT / STDERR

### Underlying technology
Using technology [namespaces](http://man7.org/linux/man-pages/man7/namespaces.7.html) docker provides isolated workspace we call container. Running Docker container creates set of namespaces for that container.

There are other technologies used for:
- controlling hardware resource - `cgroups`, 
- unifying layers to a single file system - `UnionFC`

-------------------------------------------------------------------------------
## NOTES
### Docker engine

~ add docker - docker-machine description, comparism to vm, ...

`docker info` - list docker configuration. Version, its home directory, memory, cpus and others.

`docker pull ubuntu` - find and downloads it to the docker cache. This step is redundant, because if the container will be pulled from the [docker hub](https://hub.docker.com/) with tag latest.

`docker -it ubunt /bin/bash` - runs the `bash`, interactive shell in the ubuntu image.
  - `-i` - starts an interactive container.
  - `-t` - creates a pseudo-TTY that attaches `STDIN`, `STDOUT` and `STDERR`.

`docker --rm ....` - **investigate docker --rm** - does it remove the whole image, or only its volumes? (https://docs.docker.com/engine/reference/run/#clean-up-rm)

Resources:
1. [Understanding docker](https://docs.docker.com/engine/understanding-docker/) 
