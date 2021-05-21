FROM ubuntu:18.04

# install make
RUN apt-get update
RUN apt-get -y install make
RUN apt update

# install latest git
RUN apt-get update
RUN apt install software-properties-common -y
RUN add-apt-repository ppa:git-core/ppa -y
RUN apt update
RUN apt install git -y

# install node and npm using nvm
ENV NODE_VERSION=14.15.0
RUN apt-get update
RUN apt-get -y install zip unzip curl
RUN curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash
ENV NVM_DIR=/root/.nvm
RUN . "$NVM_DIR/nvm.sh" && nvm install ${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm use v${NODE_VERSION}
RUN . "$NVM_DIR/nvm.sh" && nvm alias default v${NODE_VERSION}
ENV PATH="/root/.nvm/versions/node/v${NODE_VERSION}/bin/:${PATH}"
RUN node --version
RUN npm --version

# install yarn
RUN npm install --global yarn

# install sentry-cli
RUN curl -sL https://sentry.io/get-cli/ | bash