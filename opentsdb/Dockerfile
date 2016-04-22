FROM centos:7

MAINTAINER Michael Morello <michael.morello@gmail.com>
 
RUN yum -y install java-1.8.0-openjdk-headless.x86_64

ENV JAVA_HOME /usr/lib/jvm/jre-1.8.0-openjdk
ENV OPENTSDB_VERSION 2.2.0

ADD https://github.com/OpenTSDB/opentsdb/releases/download/v${OPENTSDB_VERSION}/opentsdb-${OPENTSDB_VERSION}.noarch.rpm .

RUN yum -y install gnuplot && \
    rpm -Uvh opentsdb-${OPENTSDB_VERSION}.noarch.rpm && \
    rm opentsdb-${OPENTSDB_VERSION}.noarch.rpm 
#RUN tar xvzf opentsdb-${OPENTSDB_VERSION}.tar.gz && rm -f opentsdb-${OPENTSDB_VERSION}.tar.gz
 
ADD logback.xml /usr/share/opentsdb/etc/opentsdb/
ADD opentsdb.conf /etc/opentsdb/opentsdb.conf

RUN useradd --home-dir /usr/share/opentsdb -M -u 31 opentsdb && \
    chown -R opentsdb:opentsdb /etc/opentsdb && \
    chown -R opentsdb:opentsdb /usr/share/opentsdb && \
    chmod 700 /etc/opentsdb

WORKDIR /usr/share/opentsdb

EXPOSE 4242

ADD run-opentsdb /

USER 31

CMD ["/run-opentsdb"]
