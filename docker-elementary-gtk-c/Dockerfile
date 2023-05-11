FROM elementary/docker:stable
LABEL net.skoona.gtk4="GTK4/C Development Container"
LABEL version="4.0.1"
LABEL target-editor="vsCode"
LABEL description="GTK4.0 Development Image based on Elementary/OS and full loaded for C development."
LABEL net.skoona.image.authors="James Scott (skoona@gmail.com)"

WORKDIR .

RUN apt-get update -y

RUN apt-get install -y apt-utils tzdata dbus vim curl wget lv htop openssh-server gnome-builder gtk-4-examples gtk-doc-tools \ 
        man-db sudo tree git sed locales x11-apps gedit whois && \
        systemctl enable ssh

ENV TZ=America/Fort_Wayne
ENV LANG=en_US.UTF-8  
ENV LANGUAGE=en_US:en  
ENV LC_ALL=en_US.UTF-8   
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime  && echo $TZ > /etc/timezone

RUN groupadd -g 1000 jscott && \
	useradd -c "James Scott III" -u 1000 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p '$y$j9T$DxhTdnP4ElhLbE9PKLOox1$5DkewQJRHVjgteT59iaVXdGkA4x8VZIyi7q/CSSqCmB' -m -s /bin/bash jscott && \
	useradd -c "James Scott Jr"  -u 1001 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p '$y$j9T$lx5JX9rvRoLgqxuRqb2.Z.$ytwddgfD0PMW.yIIf1QcBMHePaSosdbuNDFwMXKBYqA' -m -s /bin/bash skoona  && \
	useradd -c "Developer"       -u 1002 -g 1000 -G adm,lp,audio,video,dip,plugdev,sudo,users -p '$y$j9T$P5rAlM7jape.62RvYq49L/$qRJOuk5sZnpGl8iVf0dV0eXa3jpQHGoWq9/Q0oxe240' -m -s /bin/bash developer && \
	mkdir -p /etc/sudoers.d/  && \
	echo "jscott ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/jscott && \
	echo "skoona ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/skoona && \
	echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
	chmod -R 0440 /etc/sudoers.d/* && \
	mkdir /Projects && chown -R jscott:users /Projects && \ 
        sed -i "/en_US.UTF-8/s/^# //g" /etc/locale.gen && locale-gen && echo "X11UseLocalhost no" > /etc/ssh/sshd_config.d/remotexon.conf

VOLUME /Projects

EXPOSE 22
EXPOSE 5900
EXPOSE 80

ENTRYPOINT service ssh restart && bash

