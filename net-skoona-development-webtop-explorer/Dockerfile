FROM lscr.io/linuxserver/webtop:fedora-mate

ARG SC_TAG=5.0.0

LABEL net.skoona.intent="Explore WebTop Fedora Gnome Desktop Container"
LABEL net.skoona.version="${SC_TAG}"
LABEL net.skoona.target-editor="vsCode"
LABEL net.skoona.description="Fedora Gnome Desktop Image based on LinuxServer.io WebTop Project and fully loaded for development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

VOLUME /Projects
VOLUME /home
VOLUME /config

# COPY 20-start-ssh /etc/cont-init.d/20-start-ssh
COPY issue.net /etc/issue.net

RUN yum update -y &&\
	yum install -y vim curl wget lv htop man-db sudo tree net-tools  \
	openssh-server git sed gedit whois cmake flex bison gperf \
	glib2-devel gtk4-devel gnome-builder automake autoconf libtool 	 

RUN	echo "Banner /etc/issue.net" >> /etc/ssh/sshd_config.d/00-x11-enable.conf && systemctl enable sshd 

EXPOSE 22
EXPOSE 3000
EXPOSE 3001
EXPOSE 3389
