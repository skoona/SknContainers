ARG SC_JSCOTT
ARG SC_SKOONA
ARG SC_DEVELOPER

FROM golang:bullseye
LABEL net.skoona.golang="Golang Development Container"
LABEL version="3.0.0"
LABEL target-editor="vsCode"
LABEL description="GOlang Development Image based on Elementary/OS and full loaded for C development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

WORKDIR .

ENV TZ=America/Fort_Wayne
ENV LANG=en_US.UTF-8  
ENV LANGUAGE=en_US:en  
ENV LC_ALL=en_US.UTF-8   

RUN apt-get update -y && apt-get install -y apt-utils tzdata dbus vim curl wget lv htop openssh-server \ 
        man-db sudo tree git sed locales x11-apps gedit whois && \
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
	sed -i "/en_US.UTF-8/s/^# //g" /etc/locale.gen && locale-gen && \
	echo "X11UseLocalhost no" > /etc/ssh/sshd_config.d/remotexon.conf && \
	echo "Banner /etc/issue.net" >> /etc/ssh/sshd_config.d/remotexon.conf

COPY ./issue.net /etc/issue.net
COPY ./authorized_keys /home/jscott/.ssh/authorized_keys
COPY ./.bashrc /home/jscott/.bashrc
RUN chown -R jscott:jscott /home/jscott

VOLUME /Projects

EXPOSE 22
EXPOSE 5900
EXPOSE 80
EXPOSE 3000

ENTRYPOINT service ssh restart && bash
