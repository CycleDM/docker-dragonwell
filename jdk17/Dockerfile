FROM alpine:latest

ENV LANG=C.UTF-8

RUN apk add --no-cache --virtual .buildPacks wget && \
    # Dragonwell JDK
    wget -O dragonwell.tar.gz "https://github.com/alibaba/dragonwell17/releases/download/dragonwell-17.0.1.0.1+12_jdk-17.0.1-ga/Alibaba_Dragonwell_17.0.1.0.1+12_x64_alpine-linux.tar.gz" && \
    mkdir /usr/lib/java && \
    tar -xzf dragonwell.tar.gz -C /usr/lib/java --strip-components=1 && \
    # Clean
    rm dragonwell.tar.gz && \
    apk del .buildPacks

ENV JAVA_HOME=/usr/lib/java \
    CLASSPATH=.:/usr/lib/java/lib \
    PATH=/usr/lib/java/bin:$PATH

# Check version
RUN java -version && \
    javac -version

CMD ["java","-version"]