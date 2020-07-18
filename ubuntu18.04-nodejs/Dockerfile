ARG baseimage="devopsubuntu18.04:latest"
FROM ${baseimage}

COPY scripts /scripts

ENV AGENT_TOOLSDIRECTORY=/_work/_tool

RUN /scripts/installers/nodejs.sh
