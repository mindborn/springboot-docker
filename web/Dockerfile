FROM amazoncorretto:21 as dev

WORKDIR /project

# RUN yum update && yum install -y maven
RUN yum update && yum install -y tar gzip

COPY ./mvnw .
COPY ./.mvn ./.mvn/

COPY ./pom.xml .

RUN chmod +x ./mvnw

RUN ./mvnw clean package spring-boot:run || :

COPY ./src ./src/

# RUN chmod +x ./mvnw

CMD ./mvnw spring-boot:run



FROM amazoncorretto:21 as int1

WORKDIR /project

# RUN yum update && yum install -y maven
RUN yum update && yum install -y tar gzip

COPY ./mvnw .
COPY ./.mvn ./.mvn/

COPY ./pom.xml .

RUN chmod +x ./mvnw

RUN ./mvnw clean package spring-boot:run || :

COPY ./src ./src/

# RUN chmod +x ./mvnw

RUN ./mvnw package


FROM amazoncorretto:21 as prod

WORKDIR /project

COPY --from=int1 /project/target/demo-0.0.1-SNAPSHOT.jar project.jar

CMD java -jar project.jar