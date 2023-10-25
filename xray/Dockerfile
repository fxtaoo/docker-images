FROM alpine:latest

ARG VERSION=v1.8.4

RUN set -eux \
    ; apk add --no-cache ca-certificates unzip \
    && mkdir -p /var/log/xray /usr/share/xray \
    && wget -P /tmp/ "https://github.com/XTLS/Xray-core/releases/download/${VERSION}/Xray-linux-64.zip" \
    && unzip -d /usr/bin/ /tmp/Xray-linux-64.zip xray \
    && apk del unzip ; rm -f /tmp/Xray-linux-64.zip

CMD [ "/usr/bin/xray", "-config", "/etc/xray/config.json" ]
