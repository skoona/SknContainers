FROM lscr.io/linuxserver/webtop:ubuntu-mate

ARG SC_TAG=5.0.0

LABEL net.skoona.intent="WebTop Ubuntu Gnome Desktop Container"
LABEL net.skoona.version="${SC_TAG}"
LABEL net.skoona.target-editor="vsCode"
LABEL net.skoona.description="Ubuntu Gnome Desktop Image based on LinuxServer.io WebTop Project and fully loaded for development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

VOLUME /Projects
VOLUME /home
VOLUME /config

COPY 20-start-ssh /etc/cont-init.d/20-start-ssh
COPY issue.net /etc/issue.net

RUN apt-get update -y && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y apt-utils tzdata dbus vim curl wget lv htop \
	openssh-server man-db sudo tree git sed locales x11-apps gedit whois \
	libglib2.0-dev libgtk-4-dev gnome-builder gtk-4-examples gtk-doc-tools \
	net-tools cmake flex bison gperf libffi-dev libssl-dev autotools-dev automake autoconf libtool && \
	systemctl enable ssh && echo "Banner /etc/issue.net" >> /etc/ssh/sshd_config.d/00-x11-enable.conf 

EXPOSE 3000
EXPOSE 3001
EXPOSE 3389
