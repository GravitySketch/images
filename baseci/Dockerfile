FROM mono:6.8.0

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y --no-install-recommends \
        build-essential \
        redis-server \
        wget \
        unzip

RUN apt-get install -y --no-install-recommends python3
RUN apt-get install -y --no-install-recommends openjdk-8-jdk-headless

# install go
ENV GO_VERSION=1.13.5
ENV GOROOT /usr/local/go
ENV GOPATH $HOME/go
ENV GO111MODULE=on
ENV PATH $GOPATH/bin:$GOROOT/bin:$PATH
RUN wget -q https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz && \
    tar -xzf go${GO_VERSION}.linux-amd64.tar.gz && \
    rm go${GO_VERSION}.linux-amd64.tar.gz && \
    mv go /usr/local

# install maven
ENV MAVEN_VERSION 3.5.4
ENV MAVEN_HOME /usr/lib/mvn
ENV PATH $MAVEN_HOME/bin:$PATH

RUN wget http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    tar -zxvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    rm apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    mv apache-maven-$MAVEN_VERSION /usr/lib/mvn

# install protoc
ENV PROTOC_VERSION 3.10.0
RUN wget https://github.com/protocolbuffers/protobuf/releases/download/v$PROTOC_VERSION/protoc-$PROTOC_VERSION-linux-x86_64.zip && \
    unzip -o protoc-$PROTOC_VERSION-linux-x86_64.zip -d protoc3 && \
    cp -r protoc3/bin/* /usr/local/bin/ && \
    cp -r protoc3/include/* /usr/local/include/ && \
    ldconfig

# install pip3
RUN apt-get install -y --no-install-recommends python3-pip

# install redis
RUN apt-get install -y --no-install-recommends software-properties-common && \
    add-apt-repository ppa:chris-lea/redis-server && \
    apt-get update && \
    apt-get install -y --no-install-recommends redis-server
