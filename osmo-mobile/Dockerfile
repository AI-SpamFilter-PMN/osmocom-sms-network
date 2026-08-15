FROM debian:bullseye-slim

RUN sed -i 's/deb.debian.org/ftp.de.debian.org/g' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential git pkg-config libtalloc-dev \
    libgnutls28-dev libpcsclite-dev ca-certificates telnet \
    autoconf automake libtool shtool python3 \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends wget gnupg \
    && wget -qO - https://downloads.osmocom.org/packages/osmocom:/latest/Debian_11/Release.key | apt-key add - \
    && echo "deb https://downloads.osmocom.org/packages/osmocom:/latest/Debian_11/ ./" > /etc/apt/sources.list.d/osmocom-latest.list \
    && apt-get update && apt-get install -y libosmocore-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt

RUN git clone https://gitea.osmocom.org/osmocom/libosmo-gprs.git \
    && cd libosmo-gprs \
    && autoreconf -fi \
    && ./configure \
    && make \
    && make install \
    && ldconfig

RUN git clone https://gitea.osmocom.org/phone-side/osmocom-bb.git
WORKDIR /opt/osmocom-bb/src

ENV PKG_CONFIG_PATH="/usr/local/lib/pkgconfig"
RUN make nofirmware

WORKDIR /opt/osmocom-bb/src/host/layer23/src/mobile
CMD ["./mobile", "-c", "/root/.osmocom/bb/mobile.cfg"]
