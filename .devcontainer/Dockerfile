FROM golioth/golioth-ncs-base:v2.5.0-SDK-v0

# ARG NCS_VERSION=v2.5.0

SHELL ["nrfutil","toolchain-manager","launch","/bin/bash","--","-c"]
RUN \
#   # west init -m https://github.com/nrfconnect/sdk-nrf --mr ${NCS_VERSION} . \
#   # && west update --narrow -o=--depth=1
  west init -m https://github.com:golioth/zephyr-training.git west.yml
#   && west update \
#   && west zephyr-export \
#   && pip install -r deps/zephyr/scripts/requirements.txt