FROM resin/rpi-raspbian:latest

RUN apt-get update && \
  apt-get -qy install \
  i2c-tools \
  python-smbus \
  libusb-dev \
  libdbus-1-dev \
  libglib2.0-dev \
  libudev-dev \
  libical-dev \
  libreadline-dev \
  libsdl1.2-dev \
  pi-bluetooth \
  bluez \
  build-essential \
  python-pip \
  python-dev \
  python-gi \
  python-gobject \
  wget \
  && \
  wget https://github.com/parallaxinc/PropellerIDE/releases/download/0.38.5/propelleride-0.38.5-armhf.deb && \
  sh -c "dpkg -i propelleride-0.38.5-armhf.deb || true" && \
  apt-get install -y -f && \
  apt-get clean -y

RUN mkdir /controller
COPY python-controller/requirements.txt \
     /controller/
WORKDIR /controller
RUN pip install -r requirements.txt

COPY python-controller/tiny4wd.py \
     python-controller/joy.py \
     python-controller/simpleRobot.py \
     /controller/
# COPY zerobot.apt-clone.tar.gz .
# RUN apt-clone restore zerobot.apt-clone.tar.gz
COPY metabotspin/mb3.binary /mb3.binary
ENTRYPOINT []
CMD propman /mb3.binary && python tiny4wd.py
