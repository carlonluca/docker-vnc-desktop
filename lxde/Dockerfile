FROM ubuntu:jammy as system

# built-in packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt update \
    && apt install -y software-properties-common curl apache2-utils \
    && apt update \
    && apt install -y \
        supervisor nginx sudo net-tools zenity xz-utils \
        dbus-x11 x11-utils alsa-utils \
        mesa-utils libgl1-mesa-dri \
    && apt install -y \
        xvfb x11vnc \
        vim-tiny firefox \
    && apt install -y \
        lxde gtk2-engines-murrine gnome-themes-standard gtk2-engines-pixbuf \
        gtk2-engines-murrine arc-theme

RUN apt update \
    && apt autoclean -y \
    && apt autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# tini to fix subreap
ARG TINI_VERSION=v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
ADD startup.sh /
ADD supervisord.conf /etc/supervisor/conf.d/
ADD xvfb.sh /usr/local/bin/
ADD wallpapers /usr/local/share/wallpapers/

RUN chmod +x /bin/tini

WORKDIR /root
ENV HOME=/home/ubuntu \
    SHELL=/bin/bash

ENTRYPOINT ["/startup.sh"]
