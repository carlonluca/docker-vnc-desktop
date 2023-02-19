FROM debian:bullseye

# built-in packages
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update \
    && apt-get install -y \
        supervisor sudo net-tools \
        dbus-x11 x11-utils alsa-utils \
        mesa-utils libgl1-mesa-dri \
    && apt-get install -y \
        xvfb x11vnc \
    && apt-get install -y xfce4-session xfce4-goodies xfce4-panel

RUN apt-get update \
    && apt-get autoclean -y \
    && apt-get autoremove -y \
    && rm -rf /var/lib/apt/lists/*

# tini to fix subreap
ARG TINI_VERSION=v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /bin/tini
ADD startup.sh /
ADD supervisord.conf /etc/supervisor/conf.d/
ADD xvfb.sh /usr/local/bin/

RUN chmod +x /bin/tini

WORKDIR /root
ENV SHELL=/bin/bash

ENTRYPOINT ["/startup.sh"]
