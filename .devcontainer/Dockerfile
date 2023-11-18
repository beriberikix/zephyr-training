# Based on https://github.com/NordicPlayground/nrf-docker
FROM debian:stable-slim

ARG NCS_VERSION=v2.5.0
ARG NORDIC_COMMAND_LINE_TOOLS_VERSION="10-23-2/nrf-command-line-tools-10.23.2"
ARG NCS_INSTALL_DIR=/opt/toolchains/ncs-${NCS_VERSION}

# OS dependencies and packages

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  ca-certificates \
  unzip \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Install toolchain
# Make nrfutil install in a shared location, because when used with GitHub
# Actions, the image will be launched with the home dir mounted from the local
# checkout.
ENV NRFUTIL_HOME=/usr/local/share/nrfutil
RUN \
  wget -q https://developer.nordicsemi.com/.pc-tools/nrfutil/x64-linux/nrfutil \
  && mv nrfutil /usr/local/bin \
  && chmod +x /usr/local/bin/nrfutil \
  && nrfutil install toolchain-manager \
  && nrfutil install toolchain-manager search \
  && nrfutil toolchain-manager install --ncs-version ${NCS_VERSION} \
  && nrfutil toolchain-manager list

# Nordic command line tools
# Releases: https://www.nordicsemi.com/Products/Development-tools/nrf-command-line-tools/download
RUN \
  export NCLT_FILENAME="${NORDIC_COMMAND_LINE_TOOLS_VERSION}_linux-amd64.tar.gz" \
  && wget -q "https://nsscprodmedia.blob.core.windows.net/prod/software-and-other-downloads/desktop-software/nrf-command-line-tools/sw/versions-10-x-x/${NCLT_FILENAME}" \
  && mkdir -p ${NCS_INSTALL_DIR} \
  && tar -xvf ./nrf-command-line-tools-* -C ${NCS_INSTALL_DIR} --strip-components=1 \
  && ln -s ${NCS_INSTALL_DIR}/nrf-command-line-tools/bin/nrfjprog /usr/local/bin/nrfjprog \
  && ln -s ${NCS_INSTALL_DIR}/nrf-command-line-tools/bin/mergehex /usr/local/bin/mergehex \
  && rm ./nrf-command-line-tools-*

# Install Segger
RUN \
  mkdir -p /opt/SEGGER/JLink \
  && tar -xvf ${NCS_INSTALL_DIR}/JLink_*.tgz -C /opt/SEGGER/JLink --strip-components=1