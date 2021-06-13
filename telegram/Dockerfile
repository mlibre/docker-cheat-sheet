FROM debian:stable-slim

ENV HOME /home/user
RUN useradd --create-home --home-dir $HOME user \
	&& chown -R user:user $HOME \
	&& usermod -a -G audio,video user

RUN apt-get update && apt-get install -y \
    wget \
    apt-utils \
    dbus-x11 \
    dunst \
    hunspell-en-us \
    python3-dbus \
    software-properties-common \
    libx11-xcb1 \
    libpulse0 \
    gconf2 \
    libdrm2 \
    libice6 \
    libsm6 \
    libegl1-mesa-dev \
    libgl1-mesa-glx \
	  telegram-desktop \
    --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR $HOME
USER user

# COPY /usr/bin/telegram-desktop /

ENV QT_XKB_CONFIG_ROOT=/usr/share/X11/xkb

# Autorun Telegram
CMD ["/usr/bin/telegram-desktop"]
