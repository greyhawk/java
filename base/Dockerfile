# greyhawk/java:base
FROM ubuntu
MAINTAINER Greyhawk <wu.tongqing@gmail.com>

# update sources package to date
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN apt-get -y update

# install python
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -q python-software-properties software-properties-common

# install SSH server and utilities
RUN apt-get -y install openssh-server vim git sudo zip bzip2 fontconfig curl && mkdir /var/run/sshd && apt-get clean

# install oracle java from PPA
RUN add-apt-repository ppa:webupd8team/java -y
RUN apt-get -y update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get -y --force-yes install oracle-java8-installer && apt-get clean

# Set oracle java as the default java
RUN update-java-alternatives -s java-8-oracle
RUN echo "export JAVA_HOME=/usr/lib/jvm/java-8-oracle" >> ~/.bashrc
RUN echo "export PATH=$PATH:$JAVA_HOME/bin" >> ~/.bashrc

# install maven
RUN apt-get -y install maven && mkdir /root/.m2 && apt-get clean

COPY base/UnlimitedJCEPolicyJDK8 /usr/lib/jvm/java-8-oracle/jre/lib/security