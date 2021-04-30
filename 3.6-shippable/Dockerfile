# Docker container that installs Python 3.6, GDAL and necessary shippable dependencies for CI
FROM python:3.6-stretch

# Update base container install & Setup default locale
RUN apt-get update \
&& apt-get upgrade -y \
&& apt-get install -y --no-install-recommends gettext-base jq locales \
&& rm -rf /var/lib/apt/lists/* \
&& echo en_US.UTF-8 UTF-8 > /etc/locale.gen \
&& locale-gen en_US.UTF-8

# Add unstable repo to allow us to access latest GDAL builds
# Install PostGIS
RUN echo deb http://ftp.uk.debian.org/debian stable main contrib non-free >> /etc/apt/sources.list \
&& apt-get update \
&& apt-get install -y postgresql-11-postgis-2.5 \
&& rm -rf /var/lib/apt/lists/*

# Update privs to allow Postgres to run locally
RUN sed -i "s/local   all             postgres                                peer/local   all             postgres                                trust/" /etc/postgresql/11/main/pg_hba.conf

# Existing binutils causes a dependency conflict, correct version will be installed when GDAL gets intalled
RUN apt-get remove -y binutils

# Install GDAL dependencies
RUN apt-get update && apt-get install -y libgdal-dev g++

# Update C env vars so compiler can find gdal
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal

# This will install latest version of GDAL
RUN pip install GDAL==2.2.4

# Install NodeJS, for any JS work
RUN apt-get install -y --no-install-recommends nodejs npm \
&& npm i -g npm node-gyp

# Install Google Chrome for JS testing
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
&& echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" | tee /etc/apt/sources.list.d/google-chrome.list \
&& apt-get update \
&& apt-get -y install --no-install-recommends google-chrome-stable \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*


# Install awsebcli for deploying to AWS Elastic Beanstalk
RUN pip install awsebcli awscli

