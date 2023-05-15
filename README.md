# SknContainers
Implementation files for Docker development containers: Ruby, GoLang, GTK4, C++, Espressif, Arduino, and JavaScript

### Intent
- Create a full featured docker container that can be used for specific development activities, without the concerns of other langage environments.
- vsCode's SSH Remote extension is the initial IDE intended. However, eClipse, Builder, and any X11 based tooling is enabled in each container.
- Portainer is my Docker manager and the docker-compose.yml files are assumed to be used to create Stacks; while the Dockerfiles are implemented from the command-line.

### Usage
- Create a local file `.user-secrets` with the password hash of the three users in each Dockerfile
- Three users are defined in the Dockerfile which you should change as needed; the default user password is `docker`.

```bash
#!/usr/bin/env bash
#
# file: .user-secrets
#
# mkpasswd --sha-512 docker
#
export SC_JSCOTT='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_SKOONA='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_DEVELOPER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_DOCKER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
```


#### Commands
- Replace directory as needed, also change image build name. 

Build command
```bash
$ pushd $HOME/Projects/docker-elementary-gtk
$ docker build -t net-skoona-development-gtk-image:3.0.0 .
$ popd
```

See bash scripts 
- dBuild <index> <tag>
- - $ ./dBuild 0 1.0.0
or
- dMake <tage>
- - create all the dockers, and outputs `docker-compose.yml`
