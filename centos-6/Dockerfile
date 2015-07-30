FROM centos:6

# Setup environment; required by run_init
RUN mkdir -p /etc/container_environment

# EPEL and package update
RUN yum install -y epel-release
RUN yum upgrade -y

RUN mkdir -p /etc/service

# rsyslogd
RUN yum install -y rsyslog
ADD build/rsyslogd /etc/service/

# cron
ADD build/cron /etc/service/

# runit for centos6
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
