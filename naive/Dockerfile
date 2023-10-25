FROM debian:stable-slim

ARG VERSION='v118.0.5993.65-1'

RUN set -eux \
    && apt-get update && apt-get install -y wget xz-utils \
    && wget -q -O - "https://github.com/klzgrad/naiveproxy/releases/download/${VERSION}/naiveproxy-${VERSION}-linux-x64.tar.xz" | tar -xJf - -O naiveproxy-${VERSION}-linux-x64/naive > /usr/bin/naive \
    && chmod u+x /usr/bin/naive \
    && apt-get remove -y wget xz-utils \
    && apt-get clean && apt-get autoremove -y && rm -rf /var/lib/apt/lists/*

CMD ["/usr/bin/naive", "-c", "/etc/naive/config.json"]
