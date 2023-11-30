FROM ubuntu:xenial
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update && apt -y install git gnupg2 ca-certificates apt-utils apt-transport-https build-essential zlib1g-dev \
    libssl-dev libncurses5-dev libsqlite3-dev libreadline-dev libgdm-dev chromium-chromedriver

# Python 3.12.0
WORKDIR /opt/
RUN git clone --depth 1 --branch v3.12.0 https://github.com/python/cpython.git
WORKDIR /opt/cpython
RUN ./configure --enable-optimizations 
RUN make 
RUN make install
