FROM centos:7

ADD rpm /tmp

RUN rpm -Uvh /tmp/*.rpm

ADD run-tcollector /

CMD ["/run-tcollector"]
