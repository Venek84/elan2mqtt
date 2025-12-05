ARG BUILD_FROM=homeassistant/amd64-base-python:latest
FROM $BUILD_FROM

ENV ARCHIVE elan2mqtt-1.16.0

# Add env
ENV LANG C.UTF-8
ENV ELAN2MQTT_VERSION=1.16.0
ENV ARCHIVE=elan2mqtt-$ELAN2MQTT_VERSION

# Install requirements for add-on
RUN apk add --no-cache --update jq
#RUN apk add --no-cache --update python3 python3-dev py3-pip jq
RUN apk add --no-cache --update gcc g++ libc-dev python3-dev 
RUN mkdir /$ARCHIVE
RUN mkdir /$ARCHIVE/aiohttp

# Copy data for add-on
COPY run.sh /$ARCHIVE/run.sh
COPY main_worker.py /$ARCHIVE/main_worker.py
COPY socket_listener.py /$ARCHIVE/socket_listener.py
COPY aiohttp/* /$ARCHIVE/aiohttp/
COPY requirements.txt /$ARCHIVE/requirements.txt

# Let's set it to our add-on persistent data directory.
WORKDIR /$ARCHIVE

# install python packages
RUN pip install --no-cache-dir -r /${ARCHIVE}/requirements.txt

RUN ["chmod", "a+x", "./run.sh"]

CMD [ "./run.sh" ]
