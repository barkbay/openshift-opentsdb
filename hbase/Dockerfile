FROM centos:7

MAINTAINER Michael Morello <michael.morello@gmail.com>
 
RUN yum -y install java-1.8.0-openjdk-headless.x86_64 snappy

ENV JAVA_HOME /usr/lib/jvm/jre-1.8.0-openjdk
ENV HBASE_VERSION 1.1.4
 
WORKDIR /opt

ADD http://apache.mirrors.ovh.net/ftp.apache.org/dist/hbase/stable/hbase-${HBASE_VERSION}-bin.tar.gz .

RUN tar xvzf hbase-${HBASE_VERSION}-bin.tar.gz --exclude="hbase-1.1.4/docs" && rm -f hbase-${HBASE_VERSION}-bin.tar.gz 
 
ADD hbase-site.xml /opt/hbase-${HBASE_VERSION}/conf

RUN mkdir -p /data && \
    useradd --home-dir /data -M -u 30 hbase && \
    chown -R 30 /data

VOLUME ["/data"]

EXPOSE 16000 16010 16020 16030

ADD run-hbase /

COPY lib/native/libh* /usr/lib64/

USER 30

CMD ["/run-hbase"]
