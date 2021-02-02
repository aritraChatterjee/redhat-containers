### Set the base image
FROM registry.redhat.io/rhel7

### File Author / Maintainer
MAINTAINER "aritra.cnw@gmail.com"

USER root

### Set Environment
ENV JAVA_HOME="/usr/lib/jvm/java-11" \
    ADMIN_USER="admin" \
    ADMIN_PASSWORD="Admin123!" \
    JBOSS_USER="jboss" \
    JBOSS_HOME="/home/jboss/jboss-eap-7.3"

ADD jboss-eap-7.3.0.zip /tmp

RUN yum install unzip -y \
    && yum --setopt=tsflags=nodocs install -y java-11-openjdk-devel \
    && rpm -q java-11-openjdk-devel \
    && groupadd --system --gid 1001 ${JBOSS_USER} \
    && adduser --system -m -g ${JBOSS_USER} --uid 1001 ${JBOSS_USER} \
    && usermod -a -G ${JBOSS_USER} ${JBOSS_USER} \
    && unzip /tmp/jboss-eap-7.3.0.zip -d /home/jboss \
    && rm -f /tmp/jboss-eap-7.3.0.zip  \
    && $JBOSS_HOME/bin/add-user.sh $ADMIN_USER $ADMIN_PASSWORD --silent \
    && chown -R ${JBOSS_USER} /home/jboss/jboss-eap-7.3 \
    && yum clean all && [ ! -d /var/cache/yum ] || rm -rf /var/cache/yum \
    && rm -rf /tmp/*

WORKDIR /home/jboss

EXPOSE 8080 9990

USER ${JBOSS_USER}

CMD ["/home/jboss/jboss-eap-7.3/bin/standalone.sh", "-b", "0.0.0.0","-bmanagement","0.0.0.0"]
