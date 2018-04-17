FROM python:3.6-stretch

# Update base container install
RUN apt-get update
RUN apt-get upgrade -y

# Install PostGIS

RUN sed -i "s/local   all             postgres                                peer/local   all             postgres                                trust/" /etc/postgresql/10/main/pg_hba.conf
#RUN chown postgres:postgres /etc/postgresql/9.6/main/pg_hba.conf
#RUN chown postgres:postgres /etc/ssl/private/ssl-cert-snakeoil.key

# Add unstable repo to allow us to access latest GDAL builds
RUN echo deb http://ftp.uk.debian.org/debian unstable main contrib non-free >> /etc/apt/sources.list
RUN apt-get update

RUN apt-get -t unstable install -y postgresql-10-postgis-2.4

# Existing binutils causes a dependency conflict, correct version will be installed when GDAL gets intalled
RUN apt-get remove -y binutils

# Install GDAL dependencies
RUN apt-get -t unstable install -y libgdal-dev g++

# Update C env vars so compiler can find gdal
ENV CPLUS_INCLUDE_PATH=/usr/include/gdal
ENV C_INCLUDE_PATH=/usr/include/gdal

# This will install latest version of GDAL
RUN pip install GDAL>=2.2.4

# Install NodeJS, for any JS work
RUN apt-get -t unstable install -y nodejs npm
RUN npm i -g npm node-gyp

# Possibly needed
#npm install -g node-gyp
#npm install -g @angular/cli

# Install Google Chrome for JS testing
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee /etc/apt/sources.list.d/google-chrome.list
RUN apt-get update
RUN apt-get -y install google-chrome-stable
