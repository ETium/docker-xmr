FROM ubuntu:latest

LABEL maintainer="snowdream <sn0wdr1am@icloud.com>"

ENV CPULIMIT_VERSION=0.2 \
    CPU_USAGE=90 \
    XMRIG_VERSION=v6.11.0-C3 

RUN apt-get -qq update \
    &&  apt-get -qqy install --no-install-recommends wget \
    &&  apt-get -qqy install --no-install-recommends build-essential \
    &&  cd /root \
    &&  wget --no-check-certificate -c https://github.com/opsengine/cpulimit/archive/v${CPULIMIT_VERSION}.tar.gz \
    &&  tar zxvf v${CPULIMIT_VERSION}.tar.gz \
    &&  cd cpulimit-${CPULIMIT_VERSION} \
    &&  make \
    &&  cp src/cpulimit /usr/bin/ \
    &&  cd /root \
    &&  wget --no-check-certificate -c https://github.com/C3Pool/xmrig-C3/releases/download/${XMRIG_VERSION}/xmrig-${XMRIG_VERSION}-linux-Static.tar.gz?raw=true -O xmrig-${XMRIG_VERSION}-linux-Static.tar.gz \
    &&  tar zxvf xmrig-${XMRIG_VERSION}-linux-Static.tar.gz  \
    &&  cd xmrig-${XMRIG_VERSION}-linux-Static \
    &&  cp xmrig /usr/bin/ \
    &&  mkdir -p /etc/xmrig \
    &&  cp config.json /etc/xmrig \
    &&  cd /root \
    &&  apt-get -qqy remove build-essential  \
    &&  rm v${CPULIMIT_VERSION}.tar.gz \
    &&  rm -rf cpulimit-${CPULIMIT_VERSION} \
    &&  rm xmrig-${XMRIG_VERSION}-linux-Static.tar.gz  \
    &&  rm -rf xmrig-${XMRIG_VERSION}-linux-Static \
    &&  rm -rf /var/lib/apt/lists/*

COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s usr/local/bin/docker-entrypoint.sh /entrypoint.sh # backwards compat

ENTRYPOINT ["docker-entrypoint.sh"]
