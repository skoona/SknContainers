# SknContainers 
## (branch: main ) using vlans
Implementation files for Docker development containers: Ruby, GoLang, GTK4, C++, Espressif, and Arduino. Using VLans to provide each container its own ip address on the hosts local interface.


### Intent
- Create a full featured docker container that can be used for specific development activities, without the concerns of other language environments.
- vsCode's SSH Remote extension is the initial IDE intended. However, eClipse, IntelliJ, Builder, or any X11 based tooling is enabled in each container.
- Portainer is my Docker manager and the docker-compose.yml files are assumed to be used to create Stacks; while the Dockerfiles are implemented from the command-line.
- As an experiment, two containers have `lubuntu-desktop` enabled.

### Usage
There are three branches in this repo.  Each is related to the Docker Networking used.  `main` and `desktop-vlans` use `macvlan` which gives each container its own ip address. `dockert-network` uses the classic docker bridge network, where containers expose prots which are mapped to the host's ip address.

#### Prepare the build directory; copy or place into this directory (cloned root dir).
- Create a Virtual Lan(VLAN) on your network router, and enable the physical port to access it.
- - it would be helpful if Docker containers used a second interface on your docker host for this.
- Create a Docker `macvlan` network, and edit the `stack-docker-compose-*.yml` files with the network name an IPs.
- - All networking details are engaged in the docker-compose files.
- Create or edit the local file `.exports-user-secrets` with the password hash of the three users in each Dockerfile.
- - modeled after the example file `.user-secrets`, which applies a default password of `docker` to the users.
- Create or copy a `.ssh` directory, containing `authorized_keys, known_hosts, id_rsa, id_rsa.pub`, i.e full ssh setup, and to use password-less ssh logins.
- - doing so allow the container users to share a ssh public key with github; I used the dir from my docker host.
- Three users are defined in the Dockerfile which you should change as needed; the default user password is `docker`.

```bash
#!/usr/bin/env bash
#
# file: .export-user-secrets
#
# $ mkpasswd docker
#
export SC_JSCOTT='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_SKOONA='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_DEVELOPER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
export SC_DOCKER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
```

#### Build helpers
There are three bash scripts included to facilitate building a one-off{desktops}(`sBuild`) container, a single(`dBuild`) container, by index, from this collection, or (`dMake`) all containers from this collection.
In general the `sBuild` script uses the directory path to compose the image name and accept a version tag; docker-compose.yml also created from a template when a build script is run.  Review the scripts for details.


See bash scripts 
- build one-off single image: sBuild \<directory\> \<tag\>        
- - $ ./sBuild net-skoona-development-elementaary dn-1.1.0
- - $ ./sBuild net-skoona-development-ubuntu dn-1.1.0
- - create desktop enabled docker, and overwrites `docker-compose-desktop.yml`
- or
- build a single image in collection: dBuild \<index\> \<tag\>        
- - $ ./dBuild 0 dn-1.1.0
- - create single docker, and overwrites `docker-compose-devcons.yml`
- or
- build all images in collection: dMake \<tag\>     
- - $ ./dMake dn-1.1.0
- - create all the dockers, and overwrites `docker-compose-devcons.yml`


#### Create a macvlan for container networking

```bash
# Reference: https://github.com/sarunas-zilinskas/docker-compose-macvlan/tree/master
# Reference: https://www.architect.io/blog/2023-03-23/manage-networking-with-docker-compose/
$ docker network create -d macvlan --subnet=10.100.20.0/24 --gateway=10.100.20.1 -o parent=ens18.20 iot-dev-network
```


## MIT License
Let me know if this works for you!
