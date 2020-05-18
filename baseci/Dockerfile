FROM ubuntu:18.04

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

# install mono
RUN mkdir $HOME/.gnupg && \
    echo "disable-ipv6" >> $HOME/.gnupg/dirmngr.conf && \
    apt-get install -y --no-install-recommends gnupg ca-certificates && \
    apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list && \
    apt-get update && \
    apt-get -y --no-install-recommends install mono-complete

# install pip3
RUN apt-get install -y --no-install-recommends python3-pip

# install redis
RUN apt-get install -y --no-install-recommends software-properties-common && \
    add-apt-repository ppa:chris-lea/redis-server && \
    apt-get update && \
    apt-get install -y --no-install-recommends redis-server


# install latest git
RUN add-apt-repository -y ppa:git-core/ppa && \
    apt-get update && \
    apt-get install -y --no-install-recommends git

# install kubectl
ENV KUBECTL_VERSION 1.18.0
RUN apt-get install -y --no-install-recommends curl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/v$KUBECTL_VERSION/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl && \
    kubectl version --client

# install awscli
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install && \
    aws --version
