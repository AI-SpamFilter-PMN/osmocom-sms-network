FROM debian:bullseye-slim
RUN apt-get update && apt-get install -y --no-install-recommends gnupg wget ca-certificates sqlite3 telnet && rm -rf /var/lib/apt/lists/*
RUN wget -qO - https://downloads.osmocom.org/packages/osmocom:/latest/Debian_11/Release.key | apt-key add - \
    && echo "deb https://downloads.osmocom.org/packages/osmocom:/latest/Debian_11/ ./" > /etc/apt/sources.list.d/osmocom-latest.list
RUN apt-get update && apt-get install -y --no-install-recommends osmo-hlr && rm -rf /var/lib/apt/lists/*
WORKDIR /etc/osmocom
