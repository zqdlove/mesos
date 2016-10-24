FROM ubuntu:14.04.2

MAINTAINER ZhangQidong, 345804606@qq.com

#Time zone control
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

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

RUN apt-get install -y apt-transport-https

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D

RUN bash -c 'echo "# Ubuntu Precise" > /etc/apt/sources.list.d/docker.list'
RUN bash -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-precise main# Ubuntu Trusty" >> /etc/apt/sources.list.d/docker.list'
RUN bash -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main# Ubuntu Vivid" >> /etc/apt/sources.list.d/docker.list'
RUN bash -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-vivid main# Ubuntu Wily" >> /etc/apt/sources.list.d/docker.list'
RUN bash -c 'echo "deb https://apt.dockerproject.org/repo ubuntu-wily main" >> /etc/apt/sources.list.d/docker.list'

RUN apt-get update

RUN apt-get purge lxc-docker* && apt-cache policy docker-engine && \
    apt-get install -y docker-engine=1.10.3-0~trusty

RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

CMD mesos-slave --help

EXPOSE 5051
