FROM alpine:latest

ARG XRAY_VERSION=v1.7.5

RUN set -eux ; \
    apk add --no-cache ca-certificates unzip tzdata && \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime ; \
    echo "Asia/Shanghai" > /etc/timezone ; \
    mkdir -p /tmp/xray /var/log/xray /usr/share/xray /etc/xray ; \
    wget -P /etc/xray/ https://raw.githubusercontent.com/fxtaoo/docker-images/master/xray-core/config.json && \
    cd /tmp/xray ; \
    wget https://github.com/XTLS/Xray-core/releases/download/${XRAY_VERSION}/Xray-linux-64.zip && \
    unzip Xray-linux-64.zip && \
    mv xray /usr/bin ; \
    wget -P /usr/local/share/xray/ https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geoip.dat && \
    wget -P /usr/local/share/xray/ https://cdn.jsdelivr.net/gh/Loyalsoldier/v2ray-rules-dat@release/geosite.dat && \
    apk del unzip tzdata ; \
    rm -rf /tmp/xray

CMD [ "/usr/bin/xray", "-config", "/etc/xray/config.json" ]
