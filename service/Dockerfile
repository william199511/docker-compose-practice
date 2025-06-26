# 使用超轻量级的 Java 运行时
FROM gcr.io/distroless/java:8

# 环境变量（可选）
ENV APP_PORT=7081
ENV APP_ENV=test
ENV CONFIG_PATH=/opt/service/config

# 设置工作目录
WORKDIR /opt/service

# 拷贝 JAR 和配置文件
COPY iPark.jar iPark.jar
COPY config/application-test.yml config/application-test.yml

# 暴露端口
EXPOSE 7081

# 启动命令（使用 ENTRYPOINT + CMD 分离）
ENTRYPOINT ["/usr/bin/java"]
#CMD ["-Xmx512m", "-Xms512m", "-XX:MaxMetaspaceSize=256m", "-Dserver.port=7081", "-Dspring.profiles.active=test", "-Dspring.config.additional-location=file:/opt/service/config/", "-jar", "iPark.jar"]

CMD ["-Xmx512m","-Xms512m","-XX:MaxMetaspaceSize=256m", "-XX:+PrintGCDetails","-Xloggc:/opt/service/logs/gc.log","-XX:+UseGCLogFileRotation", "-XX:NumberOfGCLogFiles=5",  "-XX:GCLogFileSize=10M",  "-Dserver.port=7081",  "-Dspring.profiles.active=test",  "-Dspring.config.additional-location=file:/opt/service/config/","-jar","iPark.jar"]