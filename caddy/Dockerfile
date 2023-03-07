FROM golang:alpine

ARG XCADDY_VERSION=0.3.0
ARG CADDY_VERSION=v2.5.2

WORKDIR /tmp/xcaddy

RUN set -eux; \
    wget -c "https://github.com/caddyserver/xcaddy/releases/download/v${XCADDY_VERSION}/xcaddy_${XCADDY_VERSION}_linux_amd64.tar.gz" -O - | tar -xz \
    && ./xcaddy build ${CADDY_VERSION} \
    --with github.com/caddy-dns/cloudflare \
    --with github.com/caddyserver/replace-response


FROM alpine:latest

COPY --chmod=0755 --from=0 /tmp/xcaddy/caddy /usr/bin/caddy

RUN set -eux; \
    apk add --no-cache ca-certificates mailcap tzdata ; \
    cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime ; \
    echo "Asia/Shanghai" > /etc/timezone ; \
    apk del tzdata ; \
    mkdir -p /config/caddy /data/caddy /etc/caddy /usr/share/caddy ; \
    wget https://raw.githubusercontent.com/fxtaoo/docker-images/master/caddy/Caddyfile -P /etc/caddy;  \
    wget https://raw.githubusercontent.com/fxtaoo/docker-images/master/caddy/index.html -P /usr/share/caddy;

# See https://caddyserver.com/docs/conventions#file-locations for details
ENV XDG_CONFIG_HOME /config
ENV XDG_DATA_HOME /data

EXPOSE 80
EXPOSE 443
EXPOSE 2019

WORKDIR /srv

CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
