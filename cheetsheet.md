# Docker Cheetsheet

- `run`
- `docker ps` - list all running containers
    - `l` - list details of last added container
    - `a` - list all stopped containers
- `docker logs [container-name]` - tails logs for the container
    - `-f` - waits for further logs to be received
- `docker stop [container-name]`
- `docker inspect [container-name]` - list information about the container and its state in JSON format
    - `-f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}'` - list specified properties

