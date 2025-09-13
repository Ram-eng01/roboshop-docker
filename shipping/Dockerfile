FROM maven AS builder
WORKDIR /opt/server
COPY pom.xml .
COPY src /opt/server/src
RUN mvn clean package

FROM openjdk:17-ea-jdk-alpine3.14
EXPOSE 8080
WORKDIR /opt/server
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
COPY --from=builder /opt/server/target/shipping-*.jar /opt/server/shipping.jar
USER roboshop
CMD ["java","-jar","shipping.jar"]