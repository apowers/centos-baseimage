A Docker baseimage for CentOS, similar to https://github.com/phusion/baseimage-docker.

The purpose of this image is to provide a platform for testing configuration management
by providing a clean and fast VM-like environment.

Build It
--------

    git clone https://github.com/apowers/centos-baseimage
    cd centos-baseimage
    docker build -t centos-baseimage .

This will produce an image called centos-baseimage

Using It
----------

From your application directory start the image and get a prompt:

    docker run --rm=false --privileged -v $(pwd):/opt/app -ti centos-baseimage /sbin/run_init -- bash -l

--privileged is required for many network services to work.
