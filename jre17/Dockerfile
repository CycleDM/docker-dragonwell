FROM alpine:latest

RUN apk add --no-cache --virtual .buildPacks wget && \
    # 下载安装Dragonwell JDK
    wget -O dragonwell.tar.gz "https://github.com/alibaba/dragonwell17/releases/download/dragonwell-17.0.3.0.3+7_jdk-17.0.3-ga/Alibaba_Dragonwell_17.0.3.0.3+7_x64_alpine-linux.tar.gz" && \
    mkdir /usr/lib/java && \
    mkdir dragonwell && \
    tar -xzf dragonwell.tar.gz -C dragonwell --strip-components=1 && \
    # 生成JRE
    dragonwell/bin/jlink --module-path dragonwell/jmods --no-header-files --no-man-pages --compress=2 --add-modules ALL-MODULE-PATH --output /usr/lib/java/jre && \
    # 清理软件包
    rm dragonwell.tar.gz && \
    rm -rf dragonwell && \
    apk del .buildPacks

# 设置环境变量
ENV LANG=C.UTF-8 \
    JAVA_HOME=/usr/lib/java/jre \
    CLASSPATH=.:/usr/lib/java/jre/lib \
    PATH=/usr/lib/java/jre/bin:$PATH

# 版本检查
RUN java -version && \
    javac -version

CMD ["java","-version"]