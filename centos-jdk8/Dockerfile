FROM centos:centos7

#install node8>>
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash - && \
    yum install -y nodejs && \
#<<install node8

#install gulp>>
    npm config set registry https://registry.npm.taobao.org && \
    npm install -g gulp && \
#<<install gulp

#install jdk8>>
    yum install -y java-1.8.0-openjdk.x86_64 && \
#<<install jdk8

yum install -y wget && \

#install maven3.6>>
    wget https://www-us.apache.org/dist/maven/maven-3/3.6.0/binaries/apache-maven-3.6.0-bin.tar.gz -P /tmp && \
    tar xvf /tmp/apache-maven-3.6.0-bin.tar.gz -C /opt && \
    ln -s /opt/apache-maven-3.6.0 /opt/maven && \
#<<install maven3.6

yum install -y git autoconf automake && \

#mod timezone>>
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
#<<mod timezone

COPY maven.sh /etc/profile.d/maven.sh
