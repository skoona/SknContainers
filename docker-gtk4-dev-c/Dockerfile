FROM alpine:3.14

 LABEL "net.skoona.gtk4"="GTK4/C Development Container"
 LABEL "version"="1.0"
 LABEL "target-editor"="vsCode"
 LABEL "description"="GTK4.0 Development Image based on Alpine and full loaded for C development with X support."
 LABEL "net.skoona.image.authors"="James Scott (skoona@gmail.com)"

 ARG XDISPLAY

 WORKDIR /root/

 ENV DISPLAY=${XDISPLAY:-10.100.1.5:0.1}

 RUN apk update
 RUN apk add openssh bash bash-doc bash-completion alpine-sdk build-base g++ gcc abuild binutils binutils-doc gcc-doc util-linux pciutils usbutils coreutils findutils grep iproute2 make cmake cmake-doc extra-cmake-modules extra-cmake-modules-doc ccache ccache-doc
 RUN apk add gtk4.0 gtk4.0-dev gtk4.0-demo gtk4.0-doc 
 RUN rc-update add sshd 
 RUN setup-desktop gnome
 RUN apk add gnome-apps-extra pipewire wireplumber gst-plugin-pipewire xauth xhost xvfb
 RUN rc-update add apk-polkit-server default && rc-service apk-polkit-server start

 RUN vim curl wget lv htop build-base build-devs  pkgconfig openssh-server 
 RUN addgroup -g 1000 jscott && adduser -g “James Scott III” -u 1000 -G adm,lp,audio,wheel,input,video,netdev,users -m -s /bin/bash  jscott   jscott  && adduser -g “James Scott Jr” -u 1001  -G adm,lp,audio,wheel,input,video,netdev,users  -m -s /bin/bash skoona jscott && adduser -g “Software Architect” -u 1002 j -G adm,lp,audio,wheel,input,video,netdev,users -m -s /bin/bash developer jscott


 ENTRYPOINT [“/bin/bash”]
