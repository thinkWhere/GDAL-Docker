# GDAL-Docker

A GDAL docker container for Python 3 users.  [See the Docker Hub Page](https://hub.docker.com/r/thinkwhere/gdal-python/)

Installs and compiles the latest version of GDAL so that it can be easily added to your app via requirements.txt.

Just add the following line to requirements.txt:

```python
GDAL>=2.2.4
```

Also installs nodejs and npm to allow you to easily install any javascript dependencies. 
