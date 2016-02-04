# Reuse of https://github.com/leannenorthrop/rpi-alpine-oracle-jre 
FROM hypriot/rpi-alpine-scratch
# Set environment
ENV JAVA_VERSION=8 \
    JAVA_UPDATE=65 \
    JAVA_BUILD=17 \
    JAVA_HOME="/opt/jdk" \ 
    PATH=$PATH:${PATH}:/opt/jdk/bin
# Download and install glibc and compile/install the jdk with a bit of cleaning
RUN apk update && \
  apk upgrade && \
  apk add bash wget ca-certificates && \
  wget https://github.com/leannenorthrop/alpine-pkg-glibc/releases/download/glibc-2.22-r1-armhf-beta/glibc-2.22-r1.apk && \
  wget https://github.com/leannenorthrop/alpine-pkg-glibc/releases/download/glibc-2.22-r1-armhf-beta/glibc-bin-2.22-r1.apk && \
  wget https://github.com/leannenorthrop/alpine-pkg-glibc/releases/download/glibc-2.22-r1-armhf-beta/libgcc_s.so && \
  wget https://github.com/leannenorthrop/alpine-pkg-glibc/releases/download/glibc-2.22-r1-armhf-beta/libgcc_s.so.1 && \
  apk add --allow-untrusted glibc-2.22-r1.apk && \
  apk add --allow-untrusted glibc-bin-2.22-r1.apk && \
  mv libgcc* /lib && \
  chmod a+x /lib/libgcc_s.so* && \
  cp /usr/glibc-compat/lib/ld-linux-armhf.so.3 /lib && \
  wget --header "Cookie: oraclelicense=accept-securebackup-cookie;" "http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD}/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-arm32-vfp-hflt.tar.gz" && \
  tar -xzf jdk-${JAVA_VERSION}u${JAVA_UPDATE}-linux-arm32-vfp-hflt.tar.gz && \
  echo "" > /etc/nsswitch.conf && \ 
  mkdir /opt && \
  mv jdk1.${JAVA_VERSION}.0_${JAVA_UPDATE} /opt/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD} && \
  ln -s /opt/jdk-${JAVA_VERSION}u${JAVA_UPDATE}-b${JAVA_BUILD} /opt/jdk && \
  ln -s /opt/jdk/jre/bin/java /usr/bin/java && \
  /usr/glibc-compat/sbin/ldconfig /lib /usr/glibc-compat/lib /opt/jdk/lib /opt/jdk/jre/lib /opt/jdk/jre/lib/arm /opt/jdk/jre/lib/arm/jli && \
  echo "hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4" >> /etc/nsswitch.conf && \
  rm -f glibc-*.apk jdk*.tar.gz /opt/jdk/src.zip && \
  rm -rf $JAVA_HOME/jre/bin/jjs \
       $JAVA_HOME/jre/bin/keytool \
       $JAVA_HOME/jre/bin/orbd \
       $JAVA_HOME/jre/bin/pack200 \
       $JAVA_HOME/jre/bin/policytool \
       $JAVA_HOME/jre/bin/rmid \
       $JAVA_HOME/jre/bin/rmiregistry \
       $JAVA_HOME/jre/bin/servertool \
       $JAVA_HOME/jre/bin/tnameserv \
       $JAVA_HOME/jre/bin/unpack200 \
  apk del wget ca-certificates && \
  rm -rf /var/cache/apk/* 
ADD worker-jar-with-dependencies.jar /worker-jar-with-dependencies.jar
CMD ["java", "-jar", "/worker-jar-with-dependencies.jar"]
