#### Use latest Ubuntu LTS release as the base
FROM ubuntu:bionic

# Update base container install with GDAL dependencies
RUN apt-get update \
&& apt-get upgrade -y \
&& apt-get install -y --no-install-recommends python3-pip libgdal-dev locales \
&& locale-gen en_US.UTF-8 \
&& rm -rf /var/lib/apt/lists/*

ENV LC_ALL='en_US.utf8'

# Set python aliases for python3
RUN echo 'alias python=python3' >> ~/.bashrc
RUN echo 'alias pip=pip3' >> ~/.bashrc

# Update C env vars so compiler can find gdal
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal

# This will install latest version of GDAL
RUN pip3 install --upgrade setuptools
RUN pip3 install GDAL==2.2.4
