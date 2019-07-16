FROM node:8.15.0-alpine

#add jdk8>>
# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# add a simple script that can auto-detect the appropriate JAVA_HOME value
# based on whether the JDK or only the JRE is installed
RUN { \
		echo '#!/bin/sh'; \
		echo 'set -e'; \
		echo; \
		echo 'dirname "$(dirname "$(readlink -f "$(which javac || which java)")")"'; \
	} > /usr/local/bin/docker-java-home \
	&& chmod +x /usr/local/bin/docker-java-home
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

ENV JAVA_VERSION 8u191
ENV JAVA_ALPINE_VERSION 8.191.12-r0

RUN set -x \
	&& apk add --no-cache \
		openjdk8="$JAVA_ALPINE_VERSION" \
	&& [ "$JAVA_HOME" = "$(docker-java-home)" ]
#<< add jdk8

#add maven>>
RUN apk add --no-cache curl tar bash procps

ARG MAVEN_VERSION=3.6.0
ARG USER_HOME_DIR="/root"
ARG SHA=fae9c12b570c3ba18116a4e26ea524b29f7279c17cbaadc3326ca72927368924d9131d11b9e851b8dc9162228b6fdea955446be41207a5cfc61283dd8a561d2f
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

RUN mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha512sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/
#<< add maven

#add git >>
RUN apk --update add git less openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/* && \
#<< add git

#mod timezone>>
    apk add -U tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
#<<mod timezone

#set npm registry >>
    npm config set registry https://registry.npm.taobao.org && \
#<<set npm registry

#install gulp>>
    npm install -g gulp && \
#<<install gulp

#install yarn
    npm install -g yarn && \
    yarn config set registry https://registry.npm.taobao.org && \
#<<install yarn

#install autoconf>>
    wget http://mirrors.kernel.org/gnu/autoconf/autoconf-2.65.tar.gz && \ 
    tar -xzvf autoconf-2.65.tar.gz && \ 
    cd autoconf-2.65 && \ 
    ./configure --prefix=/usr/local && \
    make && make install
#<<install autoconf
