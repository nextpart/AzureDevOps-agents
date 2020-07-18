ARG baseimage="ubuntu:18.04"
FROM ${baseimage}

ENV DEBIAN_FRONTEND=noninteractive \
    METADATA_FILE=/image/metadata.txt \
    HELPER_SCRIPTS=/scripts/helpers

RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes && \
    mkdir /image && \ 
    mkdir agent && \
    touch /image/metadata.txt

RUN apt-get update \
    && apt-get install -y --no-install-recommends --fix-missing \
        apt-utils \
        lsb-release \ 
        lsb-core \
        software-properties-common \
        apt-transport-https \
        ca-certificates \
        gnupg \
        sqlite \
        sqlite3

COPY scripts /scripts

RUN /scripts/base/preparemetadata.sh && \
    /scripts/installers/basic.sh && \
    /scripts/base/repos.sh && \
    /scripts/helpers/apt.sh && \
    /scripts/installers/7-zip.sh && \
    /scripts/installers/azcopy.sh && \
    /scripts/installers/gcc.sh && \
    /scripts/installers/clang.sh && \
    /scripts/installers/cmake.sh && \
    /scripts/installers/build-essential.sh && \
    /scripts/installers/azure-cli.sh && \
    /scripts/installers/azure-devops-cli.sh && \
    rm -rf /scripts/installers

RUN mv /etc/services /etc/services.bak && mkdir /etc/services && mkdir /etc/services/azp

WORKDIR /etc/services/azp/

COPY ./start.sh run

CMD ["./run"]
