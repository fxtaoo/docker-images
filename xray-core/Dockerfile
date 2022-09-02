FROM alpine:latest

ARG XRAY_VERSION=v1.5.5

RUN set -eux; \
    apk add --no-cache ca-certificates unzip tzdata ; \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime ; \
    echo "Asia/Shanghai" > /etc/timezone ; \
    mkdir -p /tmp/xray /var/log/xray /usr/share/xray /etc/xray ; \
    wget https://raw.githubusercontent.com/fxtaoo/docker-images/master/xray-core/config.json -P /etc/xray/ ; \
    cd /tmp/xray \
    && wget https://github.com/XTLS/Xray-core/releases/download/${XRAY_VERSION}/Xray-linux-64.zip -P . \
    && unzip Xray-linux-64.zip \
    && mv xray /usr/bin ; mv geosite.dat /usr/share/xray/geosite.dat ; mv geoip.dat /usr/share/xray/geoip.dat ; \
    apk del unzip tzdata ; \
    rm -rf /tmp/xray

CMD [ "/usr/bin/xray", "-config", "/etc/xray/config.json" ]