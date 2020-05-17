FROM adoptopenjdk/openjdk13:jdk-13.0.2_8-alpine AS builder
WORKDIR /opt/app
COPY .mvn ./.mvn
COPY pom.xml mvnw ./
RUN ./mvnw dependency:go-offline
COPY src ./src
RUN ./mvnw install

FROM adoptopenjdk/openjdk13:jre-13.0.2_8-alpine
WORKDIR /opt/app
RUN addgroup -S spring && adduser -S spring -G spring
USER spring:spring
COPY --from=builder /opt/app/target/*.jar app.jar
ENTRYPOINT ["java","-jar","app.jar"]