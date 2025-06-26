# 使用超轻量级的 Java 运行时
FROM gcr.io/distroless/java:8

# 声明构建变量
ARG APP_ENV
ARG APP_PORT

# 环境变量（可选）
ENV APP_PORT=${APP_PORT}
ENV APP_ENV=${APP_ENV}
ENV CONFIG_PATH=/opt/service/config

# 设置工作目录
WORKDIR /opt/service

# 拷贝 JAR 和配置文件
COPY iPark.jar iPark.jar
COPY config/application-${APP_ENV}.yml config/application-${APP_ENV}.yml

# 暴露端口
EXPOSE ${APP_PORT}

# 启动命令（使用 ENTRYPOINT + CMD 分离）
ENTRYPOINT ["/usr/bin/java"]

CMD ["-Xmx512m","-Xms512m","-XX:MaxMetaspaceSize=256m", "-XX:+PrintGCDetails","-Xloggc:/opt/service/logs/gc.log","-XX:+UseGCLogFileRotation", "-XX:NumberOfGCLogFiles=5",  "-XX:GCLogFileSize=10M",  "-Dserver.port=${APP_PORT}",  "-Dspring.profiles.active=${APP_ENV}",  "-Dspring.config.additional-location=file:/opt/service/config/","-jar","iPark.jar"]
