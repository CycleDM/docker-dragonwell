FROM alpine:latest

ENV LANG=C.UTF-8

RUN apk add --no-cache --virtual .buildPacks wget && \
    # Dragonwell JDK
    wget -O dragonwell.tar.gz "https://github.com/alibaba/dragonwell17/releases/download/dragonwell-17.0.1.0.1+12_jdk-17.0.1-ga/Alibaba_Dragonwell_17.0.1.0.1+12_x64_alpine-linux.tar.gz" && \
    mkdir /usr/lib/java && \
    mkdir dragonwell && \
    tar -xzf dragonwell.tar.gz -C dragonwell --strip-components=1 && \
    dragonwell/bin/jlink --module-path dragonwell/jmods --no-header-files --no-man-pages --compress=2 --add-modules ALL-MODULE-PATH --output /usr/lib/java/jre && \
    # Clean
    rm dragonwell.tar.gz && \
    rm -rf dragonwell && \
    apk del .buildPacks

ENV JAVA_HOME=/usr/lib/java/jre
ENV CLASSPATH=.:$JAVA_HOME/lib
ENV PATH=$JAVA_HOME/bin:$PATH

CMD ["java","-version"]