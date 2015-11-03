A Docker baseimage for CentOS, similar to https://github.com/phusion/baseimage-docker.

The purpose of this image is to provide a platform for testing configuration management
by providing a clean and fast VM-like environment.

There are two baseimages, one for CentOS 6 using runit and one for CentOS 7 integrating with systemd.

# Build It

    git clone https://github.com/apowers/centos-baseimage
    cd centos-baseimage
    docker build --rm -t centos-baseimage:6 centos-6/.
    docker build --rm -t centos-baseimage:7 centos-7/.

This will produce an image called centos-baseimage

# Using It

CentOS 6
------

Start the image and get a prompt:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:6 /sbin/run_init -- bash

Start the image and run tests:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:6 /sbin/run_init -- /mnt/remote/tests/run.sh

CentOS 7
------

Start the image and get a prompt:

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:7 /sbin/run_init systemd.unit=baseimage-shell.service

Start the image and run tests: (WIP)

    docker run --rm --privileged -v $(pwd):/mnt/remote -ti centos-baseimage:7 /sbin/run_init systemd.unit=baseimage-test.service

