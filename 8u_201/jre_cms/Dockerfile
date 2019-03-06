FROM amazonlinux:2
LABEL	maintainer="rajesh.jonnalagadda@phenompeople.com" \
		version="1.8.0_201"
ARG APP_HOME=/opt/deployment
RUN	yum install wget shadow-utils tar gzip -y -q && \
	groupadd phenom -g 504 && \ 
	useradd phenom -d ${APP_HOME} -u 504
ARG JAVA_VERSION=8u201
ARG JAVA_DIR=jre1.8.0_201
ARG JAVA_BUILD=b09
RUN  wget -q -O /tmp/jre-linux-x64.tar.gz --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
      "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}-${JAVA_BUILD}/42970487e3af4f5aa5bca3f542482c60/jre-${JAVA_VERSION}-linux-x64.tar.gz"  && \
     tar -xzf /tmp/jre-linux-x64.tar.gz -C /usr/local && \
     mkdir -p /opt/deployment/dumps && \
     ln -s /usr/local/${JAVA_DIR}/bin/java /usr/local/bin && \
     ln -sf /usr/local/${JAVA_DIR} /usr/local/jre && \
     rm -rf /usr/local/${JAVA_DIR}/THIRDPARTYLICENSEREADME-JAVAFX.txt && \
     rm -rf /usr/local/${JAVA_DIR}/THIRDPARTYLICENSEREADME.txt && \
     rm -rf /usr/local/${JAVA_DIR}/COPYRIGHT && \
     rm -rf /usr/local/${JAVA_DIR}/LICENSE && \
	 rm -rf /usr/local/${JAVA_DIR}/README && \
	 rm -rf /usr/local/${JAVA_DIR}/Welcome.html && \
	 rm -rf /usr/local/${JAVA_DIR}/release && \
     rm -rf /tmp/jre-linux-x64.tar.gz
      
RUN  wget -q -O /usr/local/${JAVA_DIR}/lib/apm-agent-java.jar http://central.maven.org/maven2/co/elastic/apm/elastic-apm-agent/1.3.0/elastic-apm-agent-1.3.0.jar
ENV  JAVA_HOME=/usr/local/${JAVA_DIR}
ENV  JAVA_OPTS="$JAVA_OPTS -XX:+UseConcMarkSweepGC -XX:CMSInitiatingOccupancyFraction=75 -XX:+UseCMSInitiatingOccupancyOnly -XX:+AlwaysPreTouch -server -Xss1m -Djava.awt.headless=true -Dfile.encoding=UTF-8 \
	 -Djna.nosys=true -Djdk.io.permissionsUseCanonicalPath=true -Dio.netty.noUnsafe=true -Dio.netty.noKeySetOptimization=true -Dio.netty.recycler.maxCapacityPerThread=0 -Dlog4j.shutdownHookEnabled=false \
	 -Dlog4j2.disable.jmx=true -Dlog4j.skipJansi=true -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/opt/phenom/dumps"
ENV  LANG en_US.UTF-8
ENV  PATH=$JAVA_HOME/bin:$PATH
VOLUME /opt/deployment/dumps
ONBUILD RUN  yum update --security -q -y 