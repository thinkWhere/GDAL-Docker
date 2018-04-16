FROM python:3.5

# Configure apt to get GDAL files from testing repository
ADD docker_setup/*.pref /etc/apt/preferences.d/
ADD docker_setup/*.list /etc/apt/sources.list.d/
RUN apt-get update -y

# Install GDAL source and set compiler flags (used when pip builds GDAL)
# g++ compiler needs to be installed as gcc has already come from testing repo
RUN apt-get -t testing install -y libgdal-dev g++
ENV CFLAGS -I/usr/include/gdal

RUN pip install GDAL>=2.0.3
