FROM ubuntu:14.04.2

MAINTAINER ZhangQidong, 345804606@qq.com

#Time zone control
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

# Update the packages
RUN apt-get update 

# Install a few utility tools
RUN apt-get install -y wget tar vim

# Install the latest OpenJDK
RUN apt-get install -y openjdk-7-jre

# Install zookeeper
RUN wget https://mirrors.tuna.tsinghua.edu.cn/apache/zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz && \
    tar zxvf zookeeper-3.4.9.tar.gz && \
    rm -rf zookeeper-3.4.9.tar.gz
#    cp /zookeeper-3.4.9/conf/zoo_sample.cfg /zookeeper-3.4.9/conf/zoo.cfg && \

RUN echo "tickTime=2000" >> /zookeeper-3.4.9/conf/zoo.cfg && \
    echo "initLimit=10" >> /zookeeper-3.4.9/conf/zoo.cfg && \
    echo "syncLimit=5" >> /zookeeper-3.4.9/conf/zoo.cfg && \
    echo "dataDir=/zookeeper-3.4.9/zookeeper" >> /zookeeper-3.4.9/conf/zoo.cfg && \
    echo "clientPort=2181" >> /zookeeper-3.4.9/conf/zoo.cfg && \
    mkdir /zookeeper-3.4.9/zookeeper/ && \
    touch /zookeeper-3.4.9/zookeeper/myid

#Time zone control
RUN cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime 

CMD /zookeeper-3.4.9/bin/zkServer.sh start-foreground

EXPOSE 2181 2888 3888
