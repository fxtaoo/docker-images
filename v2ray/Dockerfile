FROM alpine:latest

ARG V2RAY_VERSION=v5.7.0

RUN set -eux \
    ; apk add --no-cache ca-certificates \
    ; mkdir -p /etc/v2ray \
    ; wget https://github.com/v2fly/v2ray-core/releases/download/${V2RAY_VERSION}/v2ray-linux-64.zip \
    && unzip -d /usr/bin v2ray-linux-64.zip v2ray \
    && rm -rf v2ray-linux-64.zip

CMD [ "/usr/bin/v2ray", "run", "-c","/etc/v2ray/config.json" ]
