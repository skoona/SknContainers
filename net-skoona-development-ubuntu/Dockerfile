FROM amd64/ubuntu:22.04

ARG SC_JSCOTT='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_SKOONA='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_DEVELOPER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_TAG=5.0.0

LABEL net.skoona.cpp="Ubuntu Gnome Desktop Container"
LABEL version="${SC_TAG}"
LABEL target-editor="vsCode"
LABEL description="Gnome Desktop xRDP Image based on Ubuntu/OS and full loaded for C development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

RUN apt-get update -y && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y apt-utils tzdata dbus vim curl wget lv htop \
	openssh-server man-db sudo tree git sed locales x11-apps gedit whois \
	net-tools gnome-session gdm3 xvfb xrdp cmake flex bison gperf libffi-dev libssl-dev \
	libglib2.0-dev libgtk-4-dev gnome-builder gtk-4-examples gtk-doc-tools gnome-shell-extensions
	
ENV TZ=America/Indiana/Indianapolis
ENV LANGUAGE=en_US:en  

RUN DEBIAN_FRONTEND=noninteractive localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 && \
	ln -snf /usr/share/zoneinfo/$TZ /etc/localtime  && echo $TZ > /etc/timezone && \
	systemctl enable ssh && systemctl set-default graphical.target

ENV LANG=en_US.UTF-8 
ENV LC_ALL=en_US.UTF-8   

# RUN rm /run/reboot-required*
RUN systemctl set-default graphical.target

# RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tasksel
# RUN DEBIAN_FRONTEND=noninteractive tasksel install ubuntu-desktop
RUN DEBIAN_FRONTEND=noninteractive apt-get install ubuntu-gnome-desktop -y
RUN rm /run/reboot-required*

RUN systemctl set-default graphical.target

RUN groupadd -g 1000 jscott && \
	useradd -c "James Scott III" -u 1000 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p ${SC_JSCOTT} -m -s /bin/bash jscott && \
	useradd -c "James Scott Jr"  -u 1001 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p ${SC_SKOONA} -m -s /bin/bash skoona  && \
	useradd -c "Developer"       -u 1002 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p ${SC_DEVELOPER} -m -s /bin/bash developer && \
	mkdir -p /etc/sudoers.d/  && \
	echo "jscott ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/jscott && \
	echo "skoona ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/skoona && \
	echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
	chmod -R 0440 /etc/sudoers.d/* && \
	mkdir /Projects && chown -R jscott:users /Projects && \ 	
	echo "X11UseLocalhost no" > /etc/ssh/sshd_config.d/00-x11-enable.conf && \
	echo "Banner /etc/issue.net" >> /etc/ssh/sshd_config.d/00-x11-enable.conf && \
	echo "Xcursor.core: 1" > /home/jscott/.Xresources && \
	sed -ibak "s/new_cursors=true/new_cursors=false/g" /etc/xrdp/xrdp.ini  && \
    adduser xrdp ssl-cert

COPY issue.net /etc/issue.net
COPY .ssh    /home/jscott/.ssh
COPY .ssh    /home/developer/.ssh
COPY .bashrc /home/jscott/.bashrc
COPY .bashrc /home/skoona/.bashrc
COPY .bashrc /home/developer/.bashrc

RUN chown -R jscott:jscott /home/jscott/.ssh && chmod 700 /home/jscott/.ssh && \
	chown jscott:jscott /home/jscott/.bashrc && chmod 644 /home/jscott/.bashrc && \
	chown -R developer:jscott /home/developer/.ssh && chmod 700 /home/developer/.ssh && \
	chown developer:jscott /home/developer/.bashrc && chmod 644 /home/developer/.bashrc && \
	chown jscott:jscott /home/jscott/.Xresources && chmod 644 /home/jscott/.Xresources 

EXPOSE 3389

VOLUME /Projects

ENTRYPOINT service xrdp restart ; service ssh restart ; bash
