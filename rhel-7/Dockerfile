FROM rhel

ENV container=docker

# EPEL and package update
RUN cd /tmp
RUN curl -O http://fedora-epel.mirror.lstn.net/7/x86_64/epel-release-7-5.noarch.rpm
RUN rpm -i epel-release-7-5.noarch.rpm
RUN yum upgrade -y

# rsyslogd and cron
#RUN yum install -y rsyslog
#RUN yum install -y cronie
#RUN yum install -y sysvinit-tools

# File system tools
#RUN yum install -y e2fsprogs

# Real systemd for centos7 ; if you want "real" systemd instead of systemd-container
RUN yum swap -y -- remove systemd-container systemd-container-libs -- install systemd systemd-libs

RUN find /lib/systemd/system/sysinit.target.wants -name 'systemd*' ! -name systemd-tmpfiles-setup.service -delete
RUN rm -f /lib/systemd/system/multi-user.target.wants/*
RUN rm -f /etc/systemd/system/*.wants/*
RUN rm -f /lib/systemd/system/local-fs.target.wants/*
RUN rm -f /lib/systemd/system/sockets.target.wants/*udev*
RUN rm -f /lib/systemd/system/sockets.target.wants/*initctl*
RUN rm -f /lib/systemd/system/basic.target.wants/*
RUN rm -f /lib/systemd/system/anaconda.target.wants/*
RUN rm -f /lib/systemd/system/plymouth*
RUN rm -f /lib/systemd/system/systemd-update-utmp*
RUN systemctl set-default multi-user.target

RUN yum clean all

# init script
RUN ln -s /usr/lib/systemd/systemd /start
ADD /build/systemd/* /etc/systemd/system/

VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
