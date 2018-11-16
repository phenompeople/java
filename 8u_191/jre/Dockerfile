FROM amazonlinux:2
LABEL	maintainer="rajesh.jonnalagadda@phenompeople.com" \
		version="1.8.0_192"
RUN	yum install wget shadow-utils tar gzip -y -q && \ 
	useradd phenom -d ${APP_HOME} -u 404 
ARG JAVA_VERSION=8u191
ARG JRE_DIR=jre1.8.0_191
ARG JAVA_BUILD=b12
ARG APP_HOME=/opt/deployment

RUN  wget -q -O /tmp/jre-linux-x64.tar.gz --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
      "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${JAVA_BUILD}/2787e4a523244c269598db4e85c51e0c/jre-${JAVA_VERSION}-linux-x64.tar.gz"  && \
     tar -xzf /tmp/jre-linux-x64.tar.gz -C /usr/local && \
     rm -f /usr/local/${JRE_DIR}/{COPYRIGHT LICENSE README THIRDPARTYLICENSEREADME.txt Welcome.html} && \
     ln -sf /usr/local/${JRE_DIR}/bin/java /usr/local/bin && \
     ln -sf /usr/local/${JRE_DIR} /usr/local/jre && \
     rm -rf /tmp/jre-linux-x64.tar.gz
RUN yum update --security -q -y
ENV JAVA_HOME=/usr/local/${JRE_DIR}
ENV LANG en_US.UTF-8
ENV PATH=$JAVA_HOME/bin:$PATH
