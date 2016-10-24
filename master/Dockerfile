FROM ubuntu:14.04.2

MAINTAINER ZhangQidong, 345804606@qq.com

#Time zone control
RUN cp  /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

# Update the packages
RUN apt-get update 

# Install a few utility tools
RUN apt-get install -y wget git tar

# Install the latest OpenJDK
RUN apt-get install -y openjdk-7-jdk

# Install autotools(Only necessary if building from git repository)
RUN apt-get install -y autoconf libtool

# Install other Mesos dependencies
RUN apt-get -y install build-essential python-dev libcurl4-nss-dev \
    libsasl2-dev libsasl2-modules maven libapr1-dev libsvn-dev

# Download Configure Build
RUN wget wget http://www.apache.org/dist/mesos/0.28.2/mesos-0.28.2.tar.gz && \
    tar -zxf mesos-0.28.2.tar.gz && \
    cd mesos-0.28.2 && \
    mkdir build && cd build && \
    ../configure && \
    make -j 30 && \
#    make check && \
    make install && \
    cd / && rm -rf /mesos-0.28.2 mesos-0.28.2.tar.gz

RUN echo "include /usr/local/lib" >> /etc/ld.so.conf && \
    /sbin/ldconfig -v

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

CMD mesos-master --help

EXPOSE 6060
