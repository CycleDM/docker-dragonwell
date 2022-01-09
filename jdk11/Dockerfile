FROM alpine:latest

ENV LANG=C.UTF-8

RUN apk add --no-cache --virtual .buildPacks wget && \
    # Dragonwell JDK
    wget -O dragonwell.tar.gz "https://github.com/alibaba/dragonwell11/releases/download/dragonwell-11.0.13.9_jdk-11.0.13-ga/Alibaba_Dragonwell_11.0.13.9_x64_alpine-linux.tar.gz" && \
    mkdir /usr/lib/java && \
    tar -xzf dragonwell.tar.gz -C /usr/lib/java --strip-components=1 && \
    # Clean
    rm dragonwell.tar.gz && \
    apk del .buildPacks

ENV JAVA_HOME=/usr/lib/java
ENV CLASSPATH=.:$JAVA_HOME/lib
ENV PATH=$JAVA_HOME/bin:$PATH

CMD ["java","-version"]