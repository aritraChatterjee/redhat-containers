### Set the base image  
FROM registry.redhat.io/rhel7 
 
### File Author / Maintainer 
MAINTAINER "Aritra Chatterjee" "aritra.chatterji@gmail.com" 

USER root

### Set Environment 			
ENV JAVA_HOME="/usr/lib/jvm/java-11" \
	JBOSS_HOME="/opt/jboss/jboss-eap-7.3" 
 
### Install EAP 7.3.0 
ADD jboss-eap-7.3.0.zip /tmp/

RUN subscription-manager register --username <uname> --password <pwd> --auto-attach \
	&& yum install unzip -y \
	&& yum --setopt=tsflags=nodocs install -y java-11-openjdk-devel \
    && rpm -q java-11-openjdk-devel \
	&& unzip /tmp/jboss-eap-7.3.0.zip -d /opt/jboss \
	&& rm -f /tmp/jboss-eap-7.3.0.zip  \
	&& $JBOSS_HOME/bin/add-user.sh admin wlisJboss! --silent \
	&& yum clean all && [ ! -d /var/cache/yum ] || rm -rf /var/cache/yum \
	&& subscription-manager unregister
 
EXPOSE 8080 9990 
 
CMD ["/opt/jboss/jboss-eap-7.3/bin/standalone.sh", "-b", "0.0.0.0","-bmanagement","0.0.0.0"]