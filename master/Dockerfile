FROM ubuntu:16.04

MAINTAINER ZhangQidong, 345804606@qq.com

#Time zone control
COPY ./localtime /etc/localtime

# Update the packages
RUN apt-get update

# Install a few utility tools
RUN apt-get install -y wget git tar

# Install the latest OpenJDK
RUN apt-get install -y openjdk-8-jdk

# Install autotools(Only necessary if building from git repository)
RUN apt-get install -y autoconf libtool

# Install other Mesos dependencies
RUN apt-get -y install build-essential python-dev python-six \
    python-virtualenv libcurl4-nss-dev libsasl2-dev libsasl2-modules \
    maven libapr1-dev libsvn-dev zlib1g-dev

# Download Configure Build
#RUN wget http://www.apache.org/dist/mesos/1.3.0/mesos-1.3.0.tar.gz
     tar -zxf mesos-1.3.0.tar.gz && \
     cd mesos-1.3.0 && \
     mkdir build && cd build && \
     ../configure && \
     make && \
     make check && \
     make install && \
    cd / && rm -rf /mesos-1.3.0 mesos-1.3.0.tar.gz

RUN echo "include /usr/local/lib" >> /etc/ld.so.conf && \
    /sbin/ldconfig -v

CMD mesos-master --help

EXPOSE 5050
