FROM debian:jessie

RUN echo \
'deb http://archive.debian.org/debian jessie main contrib non-free \n\
deb http://archive.debian.org/debian-security jessie/updates main contrib non-free \n\
deb-src http://archive.debian.org/debian jessie main contrib non-free \n\
deb-src http://archive.debian.org/debian-security jessie/updates main contrib non-free' > /etc/apt/sources.list

# Deps
RUN apt update 
RUN apt-get build-dep -y --force-yes python3
RUN apt-get install -y --force-yes build-essential gdb lcov pkg-config libbz2-dev libffi-dev libgdbm-dev \
    liblzma-dev libncurses5-dev libreadline6-dev libsqlite3-dev libssl-dev lzma lzma-dev tk-dev uuid-dev libjpeg-dev \
    zlib1g-dev git fonts-liberation libasound2 libatk-bridge2.0-0 libatk1.0-0 libatspi2.0-0 wget libcairo2 libcups2 \
    libdbus-1-3 libgtk-3-0 libgbm1 libnspr4 libnss3 libpango-1.0-0 libxkbcommon0 xdg-utils apt-transport-https gnupg2

# OpenSSL 1.1.1
# this is a dependency of python 3.12.0 
WORKDIR /opt
ADD https://www.openssl.org/source/openssl-1.1.1w.tar.gz /opt
RUN mkdir /opt/openssl && tar -xf openssl-1.1.1w.tar.gz -C /opt/openssl --strip-components=1
WORKDIR /opt/openssl
RUN ./config && make && make install
RUN ldconfig

# Python 3.12.0
WORKDIR /opt/
RUN git clone --depth 1 --branch v3.12.0 https://github.com/python/cpython.git
WORKDIR /opt/cpython
RUN ./configure 
RUN make 
RUN make install
RUN echo "1"