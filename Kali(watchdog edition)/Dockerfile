FROM kalilinux/kali-linux-docker

# Dockerfile author / maintainer 
MAINTAINER Watchdog1023

#Update the Container
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get dist-upgrade -y
RUN apt-get clean

#Getting Build Tools
RUN apt-get install git build-essential x11vnc autoconf automake libtool-bin -y

#Getting VNC Compoundents
RUN apt-get install git x11vnc tightvncserver python gnome-core -y

#Getting Pen-Testing Tools
RUN apt-get install nmap set aircrack-ng tor metasploit-framework proxychains exploitdb fcrackzip sqlmap john hydra macchanger rainbowcrack wordlists wpscan crunch apache2  wireshark postgresql -y
RUN apt-get clean

#Getting Utils
RUN apt-get install p7zip-full unrar unzip -y
RUN apt-get clean

#Installing Can-Utils for CAN exploiting
RUN git clone https://github.com/linux-can/can-utils.git
WORKDIR can-utils/
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install
WORKDIR /
RUN rm -vr can-utils

#Getting Network Tools
RUN apt-get install net-tools

#Cleaning up Build Tools
RUN apt-get autoremove -y
RUN apt-get clean

#Adding xwindows user
ENV USER root

#Adding VNC Tools
ADD .vnc /root/.vnc
ADD .Xauthority /root/.Xauthority
ADD startup.sh /startup.sh

#Getting VNC Autostart Tools
RUN git clone https://github.com/novnc/noVNC.git /root/noVNC
RUN git clone https://github.com/novnc/websockify.git /root/noVNC/utils/websockify
RUN chmod 0755 /startup.sh
RUN ./startup.sh

#Getting ENV Ready for use
RUN service postgresql start
RUN serive tor start
RUN update-rc.d postgresql enable
RUN update-rc.d tor enable

#Making VNC Ports Avilable
EXPOSE 5920 5901 6080

#Start a Bash Terminal
CMD bash