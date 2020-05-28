# Docker container that installs Python 3.6, GDAL and necessary shippable dependencies for CI
FROM thinkwhere/gdal-python:gdal3.0.4-py3.8

# Update base container install
RUN apt-get update \
&& apt-get install -y wget apt-utils

## Install PostGIS
RUN apt -y install gnupg2 \
&& wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
&& echo "deb http://apt.postgresql.org/pub/repos/apt/ focal-pgdg main" | tee  /etc/apt/sources.list.d/pgdg.list \
&& apt-get update \
&& apt-get install -y postgresql-11-postgis-2.5

#
## Update privs to allow Postgres to run locally
RUN sed -i "s/local   all             postgres                                peer/local   all             postgres                                trust/" /etc/postgresql/11/main/pg_hba.conf
#
## Existing binutils causes a dependency conflict, correct version will be installed when GDAL gets intalled
RUN apt-get remove -y binutils

#
## Install NodeJS, for any JS work
RUN apt-get install -y nodejs npm \
&& npm i -g npm node-gyp

#
## Install Google Chrome for JS testing
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
&& echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee /etc/apt/sources.list.d/google-chrome.list \
&& apt-get update \
&& apt-get -y install google-chrome-stable


#
## Install awsebcli for deploying to AWS Elastic Beanstalk
RUN pip3 install awsebcli
