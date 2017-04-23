FROM debian:8
MAINTAINER Jeremy Nicklas <jeremywnicklas@gmail.com>

# Install dependencies
RUN export DEBIAN_FRONTEND=noninteractive \
  && apt-get update && apt-get install --yes --no-install-recommends \
    build-essential \
    python-dev \
    python-qt4 \
    python-pip \
  && rm -fr /var/lib/apt/lists/* \
  && pip2 install https://electrum-ltc.org/download/Electrum-LTC-2.6.4.2.tar.gz

ENV QT_X11_NO_MITSHM 1

ENV HOME /data

WORKDIR ${HOME}

ENTRYPOINT [ "electrum-ltc" ]
