FROM amazonlinux:2
LABEL	maintainer="rajesh.jonnalagadda@phenompeople.com" \
		version="1.8.0_201"
ARG APP_HOME=/opt/deployment
RUN	yum install wget shadow-utils tar gzip -y -q && \ 
	useradd phenom -d ${APP_HOME} -u 1004
ARG JAVA_VERSION=8u201
ARG JAVA_DIR=jdk1.8.0_201
ARG JAVA_BUILD=b09

RUN  wget -q -O /tmp/jdk-linux-x64.tar.gz --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
      "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${JAVA_BUILD}/42970487e3af4f5aa5bca3f542482c60/jdk-${JAVA_VERSION}-linux-x64.tar.gz"  && \
     tar -xzf /tmp/jdk-linux-x64.tar.gz -C /usr/local && \
     ln -sf /usr/local/${JAVA_DIR}/bin/java /usr/local/bin && \
     ln -sf /usr/local/${JAVA_DIR} /usr/local/jdk && \
  	 rm -rf /tmp/jdk-linux-x64.tar.gz
RUN  rm -f /usr/local/jdk/release /usr/local/jdk/javafx-src.zip && \
	 rm -f /usr/local/jdk/COPYRIGHT /usr/local/jdk/src.zip && \
	 rm -f /usr/local/jdk/README.html /usr/local/jdk/LICENSE && \
	 rm -f /usr/local/jdk/THIRDPARTYLICENSEREADME.txt /usr/local/jdk/THIRDPARTYLICENSEREADME-JAVAFX.txt && \
	 rm -f /usr/local/jdk/Welcome.html
RUN  rm -f /usr/local/jdk/jre/COPYRIGHT /usr/local/jdk/jre/LICENSE /usr/local/jdk/jre/README && \
	 rm -f /usr/local/jdk/jre/THIRDPARTYLICENSEREADME.txt /usr/local/jdk/jre/THIRDPARTYLICENSEREADME-JAVAFX.txt && \ 
	 rm -f /usr/local/jdk/jre/Welcome.html
RUN  wget -q -O /usr/local/${JAVA_DIR}/lib/apm-agent-java.jar http://central.maven.org/maven2/co/elastic/apm/elastic-apm-agent/1.3.0/elastic-apm-agent-1.3.0.jar
ENV  JAVA_HOME=/usr/local/${JAVA_DIR}
ENV  LANG en_US.UTF-8
ENV  PATH=$JAVA_HOME/bin:$PATH
ONBUILD RUN  yum update --security -q -y 
