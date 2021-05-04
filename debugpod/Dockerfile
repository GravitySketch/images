FROM ubuntu:18.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --no-install-recommends \
        build-essential \
        wget \
        unzip \
        curl \
	ssh \
        iputils-ping \
        apt-transport-https \
        ca-certificates \
        gnupg-agent

# install redis
RUN apt-get install -y --no-install-recommends software-properties-common && \
    add-apt-repository ppa:chris-lea/redis-server && \
    apt-get update && \
    apt-get install -y --no-install-recommends redis-server

# Install postgres client
RUN wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main" > /etc/apt/sources.list.d/pgdg.list
RUN apt-get update
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y \
    postgresql-client-10
