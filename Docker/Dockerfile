FROM amazon/aws-cli

MAINTAINER Dirk Piethan

RUN yum install openssh-clients unzip -y
RUN curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/linux_64bit/session-manager-plugin.rpm" -o "session-manager-plugin.rpm"
RUN yum install -y session-manager-plugin.rpm

COPY ssh/ /root/.ssh

