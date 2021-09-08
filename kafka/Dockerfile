FROM centos:centos7 as build-stage

RUN yum update -y && yum install wget which java-1.8.0-openjdk-devel -y && yum clean all

RUN wget -O kafka-2.4.1.30.tar.gz https://github.com/linkedin/kafka/archive/refs/tags/2.4.1.30.tar.gz && \
    tar zxvf kafka-2.4.1.30.tar.gz && \
    rm kafka-2.4.1.30.tar.gz && \
    cd kafka-2.4.1.30 && \
    sed -i 's/version=2.4.2-SNAPSHOT/version=2.4.1.30/g' gradle.properties && \
    ./gradlew clean releaseTarGz

FROM scratch AS export-stage
COPY --from=build-stage /kafka-2.4.1.30/core/build/distributions/kafka_2.12-2.4.1.30.tgz /
