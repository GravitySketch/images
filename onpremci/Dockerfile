FROM cypress/browsers:node14.15.0-chrome86-ff82

RUN apt-get update
RUN apt-get upgrade -y

# install java 11
RUN apt-get install -y gnupg2
RUN apt-get install -y --no-install-recommends software-properties-common
RUN wget -qO - https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public | apt-key add -
RUN add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/
RUN apt-get install -y --no-install-recommends adoptopenjdk-11-hotspot
