FROM centos:centos7 as build-stage

RUN yum update -y
#RUN yum -y install epel-release && yum -y update && yum clean all
RUN yum groupinstall -y "Development Tools"
#RUN yum -y install wget
#RUN wget -O - https://github.com/jemalloc/jemalloc/releases/download/5.2.1/jemalloc-5.2.1.tar.bz2 | tar -xj && \
#    cd jemalloc-5.2.1 && \
#    ./configure && \
#    make && \
#    make install

COPY jemalloc-5.2.1.tar.bz2 .

RUN tar -xjvf jemalloc-5.2.1.tar.bz2 \
    && cd jemalloc-5.2.1 \
    && ./configure --prefix=/target/jemalloc \
    && make \
    && make install

FROM scratch AS export-stage
COPY --from=build-stage /target/jemalloc /jemalloc
