FROM arm32v7/node:15.3.0
USER root
RUN mkdir -p /usr/src/node-red

# User data directory, contains flows, config and nodes.
RUN mkdir /data

WORKDIR /usr/src/node-red


# package.json contains Node-RED NPM module and node dependencies
COPY package.json /usr/src/node-red/
RUN npm install

RUN apt-get update
RUN apt-get dist-upgrade -y

RUN apt-get install -y \
    build-essential \
    python \ 
    wget \
    build-essential \
    python-dev \
    mercurial \
    python-dev \
    python-pip \
    python-virtualenv

RUN  pip install RPi.GPIO 

RUN hg clone http://hg.code.sf.net/p/raspberry-gpio-python/code /raspberry-gpio-python-code
#WORKDIR  /usr/src/node-red/raspberry-gpio-python-code
#RUN  python setup.py install
#RUN rm /usr/src/node-red/raspberry-gpio-python-code


# User configuration directory volume
VOLUME ["/data"]
EXPOSE 1880

# Environment variable holding file path for flows configuration
ENV FLOWS=flows.json

CMD ["npm", "start", "--", "--userDir", "/data"]