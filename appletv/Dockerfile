# Docker file to create an image for a hass.io add-on that contains enough software to listen to events via RTL_SDR/RTL_433 and then publish them to a MQTT broker.
# The script resides in a volume and can be modified to meet your needs.
# This hass.io addon is based on Chris Kacerguis' project here: https://github.com/chriskacerguis/honeywell2mqtt,
# which is in turn based on Marco Verleun's rtl2mqtt image here: https://github.com/roflmao/rtl2mqtt

# IMPORTANT: The container needs privileged access to /dev/bus/usb on the host.

ARG BUILD_FROM
FROM $BUILD_FROM

ENV LANG C.UTF-8

MAINTAINER Brett Clark

LABEL Description="This image is used to install pyatv"

#
# First install software packages needed to compile openssl for pyatv
#
RUN apk add --no-cache --virtual build-deps python3-dev wget alpine-sdk git  && \
    mkdir /tmp/appletv && \
    cd /tmp/appletv && \
    git clone https://github.com/openssl/openssl && \
    cd /tmp/appletv/openssl && \
    ./config && \
    make && \
    make install && \
    cd /tmp/appletv && \
    wget https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    pip3 install pyatv && \
    rm -r /tmp/appletv

#
# Define an environment variable
#
# Use this variable when creating a container to specify the MQTT broker host.

