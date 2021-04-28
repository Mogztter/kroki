FROM node:14-alpine

ENV DRAWIO_VERSION "14.5.1"

RUN apk --update --no-cache add --virtual build-dependencies git

RUN git clone https://github.com/jgraph/drawio-desktop.git \
    && cd drawio-desktop \
    && git checkout --quiet v$DRAWIO_VERSION \
    && git submodule init \
    && git submodule update \
    && npm i

#RUN ./drawio-desktop/node_modules/.bin/electron drawio/src/main/webapp --version

RUN apk del build-dependencies
