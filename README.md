# SknContainers
Implementation files for Docker development containers: Ruby, GoLang, GTK4, C++, Espressif, Arduino, and JavaScript

### Intent
- Create a full featured docker container that can be used for specific development activities, without the concerns of other langage environments.
- vsCode's SSH Remote extension is the initial IDE intended. However, eClipse, Builder, and any X11 based tooling is enabled in each container.
- Portainer is my Docker manager and the docker-compose.yml files are assumed to be used to create Stacks; while the Dockerfiles are implemented from the command-line.

### Usage
Replace directory as needed, also change image build name. Three users are defined in the Dockerfile which you should change as needed; the default user password is `docker`.

Build command
```bash
$ pushd $HOME/Projects/docker-elementary-gtk
$ docker build -t net-skoona-development-gtk-image:3.0.0 .
$ popd
```
