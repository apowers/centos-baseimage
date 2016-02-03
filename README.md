A Docker baseimage for CentOS, similar to https://github.com/phusion/baseimage-docker.

The purpose of this image is to provide a platform for testing configuration management
by providing a clean and fast VM-like environment.

There are two baseimages, one for CentOS 6 using runit and one for CentOS 7 integrating with systemd.

# Build It

    git clone https://github.com/apowers/centos-baseimage
    cd centos-baseimage
    docker pull centos:7
    docker build --rm -t centos-baseimage:6 centos-6/.
    docker build --rm -t centos-baseimage:7 centos-7/.

This will produce an image called centos-baseimage

## For Red Hat
The build is slightly different, use the appropiate names appropriatly. Note that rhel is rhel so it won't work "out of the box". After the build add your rhel-base repo then install rsyslog and cronie and commit.

    docker pull rhel
    docker pull rhel6
    docker build --rm -t rhel-baseimage:6 rhel-6/.
    docker build --rm -t rhel-baseimage:7 rhel-7/.

# Using It

CentOS 6
------

Start the image and get a prompt:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:6 /sbin/run_init -- bash

Start the image and run tests:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:6 /sbin/run_init -- /mnt/remote/tests/run_tests.sh

CentOS 7
------

Start the image and get a prompt:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:7 /usr/lib/systemd/systemd --unit=baseimage-shell.service

Start the image and run tests: (WIP)
* test script must be "$(pwd)/test/run_tests.sh" as defined in centos-7/build/systemd/baseimage-test.service

    docker run --rm --privileged -e "TEST=<some_value>" -v $(pwd):/mnt/remote -ti centos-baseimage:7 /usr/lib/systemd/systemd --unit=baseimage-test.service

BUGS:
* test script doesn't use docker environment value
* docker exit code doesn't reflect exit status of tests
