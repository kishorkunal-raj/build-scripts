FROM centos:7
ARG JAVA_VERSION=11
ARG TARGETPLATFORM


MAINTAINER "Vijay Kumar H P <vijaykh1@in.ibm.com>"

RUN yum -y update \
    && yum -y install java-${JAVA_VERSION}-openjdk-headless openssl bind-utils \
    && yum -y clean all

#####
# Add Tini
#####
ENV TINI_VERSION v0.19.0
ENV TINI_SHA256_AMD64=93dcc18adc78c65a028a84799ecf8ad40c936fdfc5f2a57b1acda5a8117fa82c
ENV TINI_SHA256_PPC64LE=3f658420974768e40810001a038c29d003728c5fe86da211cff5059e48cfdfde

RUN set -ex; \
    if [[ ${TARGETPLATFORM} = "linux/ppc64le" ]]; then \
        curl -s -L https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini-ppc64le -o /usr/bin/tini; \
        echo "${TINI_SHA256_PPC64LE} */usr/bin/tini" | sha256sum -c; \
        chmod +x /usr/bin/tini; \
    else \
        curl -s -L https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini -o /usr/bin/tini; \
        echo "${TINI_SHA256_AMD64} */usr/bin/tini" | sha256sum -c; \
        chmod +x /usr/bin/tini; \
    fi

