FROM debian:stretch

RUN echo \
'deb http://archive.debian.org/debian stretch contrib main non-free \n\
deb-src http://archive.debian.org/debian stretch contrib main non-free \n\
deb http://archive.debian.org/debian-security stretch/updates contrib main non-free \n\
deb-src http://archive.debian.org/debian-security stretch/updates contrib main non-free' > /etc/apt/sources.list

# Deps
RUN apt update 
RUN apt-get build-dep -y python3
RUN apt-get install -y build-essential gdb lcov pkg-config libbz2-dev libffi-dev libgdbm-dev \
    liblzma-dev libncurses5-dev libreadline6-dev libsqlite3-dev libssl-dev lzma lzma-dev tk-dev \
    uuid-dev zlib1g-dev git libatk-bridge2.0-0 libgbm1 libgtk-3-0 libxkbcommon0 fonts-liberation \
    libasound2 libnspr4 libnss3 wget xdg-utils apt-transport-https gnupg2 software-properties-common

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
RUN ./configure --enable-optimizations
RUN make
RUN make install
