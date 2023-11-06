FROM golioth/golioth-zephyr-base:0.16.3-SDK-v0

RUN \
  apt-get -y update \
  && apt-get -y install --no-install-recommends \
  wget \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*