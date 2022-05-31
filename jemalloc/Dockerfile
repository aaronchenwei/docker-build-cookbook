FROM centos:centos7 as build-stage

ENV JEMALLOC_VERSION=5.3.0

RUN yum update -y
#RUN yum -y install epel-release && yum -y update && yum clean all
RUN yum groupinstall -y "Development Tools"
RUN yum -y install wget
RUN wget -O - https://github.com/jemalloc/jemalloc/releases/download/${JEMALLOC_VERSION}/jemalloc-${JEMALLOC_VERSION}.tar.bz2 | tar -xj
RUN cd jemalloc-${JEMALLOC_VERSION} && \
   ./configure --prefix=/target/jemalloc && \
   make && \
   make install

# COPY jemalloc-5.2.1.tar.bz2 .

# RUN tar -xjvf jemalloc-5.2.1.tar.bz2 \
#     && cd jemalloc-5.2.1 \
#     && ./configure --prefix=/target/jemalloc \
#     && make \
#     && make install

FROM scratch AS export-stage

ENV JEMALLOC_VERSION=5.3.0

COPY --from=build-stage /target/jemalloc /${JEMALLOC_VERSION}
