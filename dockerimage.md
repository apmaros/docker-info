# Dockerfile

**description**

## Instructions

### FROM
Base image for the image. Typically, it is OS, or framework pulled from [docker hub](https://hub.docker.com/).

`FROM ubuntu:14.04`

### MAINTAINER
Author of the generated image

`MAINTAINER superman <superman@krypton.com>`

### RUN
Executes any command and commits changes to the image creating a new layer on the top of current image. This image is used in the next step in Dockerfile. RUN commands should be small, as layering small and cheap.o

### CMD
Provides defaults for an executing container. It runs the instruction in the image with arguments.

- exec form - `CMD ["apache2","-DFOREGROUND"]`
- shell form - `CMD apache -DFOREGROUND` 

In case these defaults include an executable, `ENTRYPOINT` must by specified too.

### Expose
Indicates the ports on which a container will listen for connections. Expose does not make these ports available outside of the container. Flags `-p` and `-P` publish exposed ports.

`EXPOSE <port> [<port>...]`

### Env
Sets environmental variable

`ENV PG_MAJOR 9.3`

### ADD or COPY
`Copy` is preferred due its transparency. It copies local files into the container. `ADD` has additional functionality such as tar extraction and remote URL support.

`COPY requirements.txt /tmp/`

It is discouraged to use  `ADD` to fetch packages from remote URL. Use of `curl`, or `wget` is preferred alternative.

### ENTRYPOINT
Allows to configure the container that will run as an executable. It present the default commands and arguments, which can be appended with further args from `CMD`.

``
FROM ubuntu
ENTRYPOINT ["top", "-b"]
CMD ["-c"]
``

ENTRYPOINT can be overridden using `docker run --entrypoint` flag.

Arguments passed in `docker run`, e.g. `docker run -i -t --rm -p 80:80 nginx
` will append the `ENTRYPOINT` arguments and overwrite arguments specified in `CMD`

### VOLUME
Creates a mount point with specified name and mark it as externally mounted volume. Volume should be used for any mutable storage of data including databases, Kafka brokers and others.

`VOLUME ["/data"]`

### USER
Sets user name or UID to see when running image or executable within container. It is discouraged to use `sudo` due to its unpredictable `TTY` signals.

USER daemon

### WORKDIR
Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY` and `ADD` command. It can be used multiple times in `Dockerfile`.  Its advised to use absolute paths to prevent confusion.

`
ENV DIRPATH /path
WORKDIR $DIRPATH/$DIRNAME
RUN pwd
`

### ONBUILD
command executes after the current Dockerfile build completes.
