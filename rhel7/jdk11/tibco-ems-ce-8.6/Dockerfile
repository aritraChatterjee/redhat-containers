### Set the base image  
FROM registry.redhat.io/rhel7 
 
### File Author / Maintainer 
MAINTAINER "Aritra Chatterjee" "aritra.cnw@gmail.com" 

USER root

### Set Environment 			
ENV JAVA_HOME="/usr/lib/jvm/java-11"
 
### Install tibco 8.6.0 
ADD TIB_ems-ce_8.6.0_linux_x86_64.zip /tmp/

RUN yum install unzip -y \
	&& yum --setopt=tsflags=nodocs install -y java-11-openjdk-devel \
    && rpm -q java-11-openjdk-devel \
	&& unzip /tmp/TIB_ems-ce_8.6.0_linux_x86_64.zip -d /tmp \
	&& cd /tmp/TIB_ems-ce_8.6.0 \
	&& yum install -y rpm/*.rpm \
	&& mkdir /opt/tibco/datastore \
	&& chmod -R 777 /opt/tibco \
	&& yum clean all && [ ! -d /var/cache/yum ] || rm -rf /var/cache/yum

WORKDIR /opt/tibco
 
EXPOSE 7222

CMD ["/opt/tibco/ems/8.6/bin/tibemsd","-config", "/opt/tibco/ems/8.6/samples/config/tibemsd.conf"]
