# Base Ubuntu Precise 12.04 LTS image
#
FROM ubuntu:precise
MAINTAINER amplab amp-docker@eecs.berkeley.edu

# Setup a volume for data
VOLUME ["/data"]

# Set correct source list
RUN echo "deb http://archive.ubuntu.com/ubuntu precise main universe" > /etc/apt/sources.list

# install a few other useful packages plus Open Jdk 7
RUN apt-get update && apt-get upgrade -y && apt-get install -y less openjdk-7-jre-headless net-tools vim-tiny sudo openssh-server iputils-ping

# Install Hadoop
ADD http://mirror.sdunix.com/apache/hadoop/common/hadoop-1.2.1/hadoop_1.2.1-1_x86_64.deb /root/
RUN dpkg -i /root/hadoop_1.2.1-1_x86_64.deb
RUN rm /root/hadoop_1.2.1-1_x86_64.deb

# add Hadoop config file templates
# NOTE: we rather do this as a single ADD statement
# since we are running into
#       Error build: Unable to mount using aufs
#       Unable to mount using aufs
# issue. For more information see
#       https://github.com/dotcloud/docker/issues/1171
ADD files /root/hadoop_files

# Set JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
