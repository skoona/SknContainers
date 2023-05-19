FROM x11docker/gnome

ARG SC_JSCOTT='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_SKOONA='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_DEVELOPER='$y$j9T$bX33CvQOJHRg17OWhTjja.$2Dk/Jhfeu78DyJXpPc2Op58V7bpRbfUazFOHRFSlyq4'
ARG SC_TAG=5.0.1

LABEL net.skoona.cpp="X11 Docker Gnome Desktop Container"
LABEL version="${SC_TAG}"
LABEL target-editor="vsCode"
LABEL description="X11docker Gnome Image - fully loaded for C development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

WORKDIR /

ENV TZ=America/Fort_Wayne
ENV LANG=en_US.UTF-8  
ENV LANGUAGE=en_US:en  
ENV LC_ALL=en_US.UTF-8   

RUN apt-get update -y && \
	DEBIAN_FRONTEND=noninteractive apt-get install -y apt-utils tzdata dbus vim curl wget lv htop \
	openssh-server man-db sudo tree git sed locales x11-apps gedit whois \
	net-tools x11vnc xvfb xrdp flex bison gperf libffi-dev libssl-dev \
	libglib2.0-dev gnome-builder gtk-doc-tools gnome-shell-extensions \
	net-tools flex bison gperf libffi-dev libssl-dev && \
	systemctl enable ssh && \
	ln -snf /usr/share/zoneinfo/$TZ /etc/localtime  && echo $TZ > /etc/timezone

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
	sed -i "/en_US.UTF-8/s/^# //g" /etc/locale.gen && DEBIAN_FRONTEND=noninteractive locale-gen && \
	echo "X11UseLocalhost no" > /etc/ssh/sshd_config.d/00-x11-enable.conf && \
	echo "Banner /etc/issue.net" >> /etc/ssh/sshd_config.d/00-x11-enable.conf && \
	echo "Xcursor.core: 1" > /home/jscott/.Xresources 

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

ENTRYPOINT service ssh restart ; bash
