FROM rhel6

# Setup environment; required by run_init
RUN mkdir -p /etc/container_environment

# EPEL and package update
RUN cd /tmp
RUN curl -O http://fedora-epel.mirror.lstn.net/6/x86_64/epel-release-6-8.noarch.rpm
RUN rpm -i epel-release-6-8.noarch.rpm
RUN yum upgrade -y

RUN mkdir -p /etc/service

# rsyslogd
#RUN yum install -y rsyslog
ADD build/rsyslogd /etc/service/

# cron
#RUN yum install -y cronie
ADD build/cron /etc/service/

# runit
ADD build/bin/packagecloud.imeyer.runit.sh /tmp/
RUN /tmp/packagecloud.imeyer.runit.sh
RUN yum install -y runit
RUN mkdir -p /etc/runit
ADD build/runit/* /etc/runit/

# Custom runit starter
RUN yum install -y python python-argparse
ADD /build/bin/run_init /sbin/

RUN yum clean all

CMD ["/sbin/run_init"]
