FROM golang:alpine

ARG VERSION=v2.7.4
ARG XCADDY_VERSION=0.3.5

WORKDIR /tmp/xcaddy

RUN set -eux \
    ; wget -c "https://github.com/caddyserver/xcaddy/releases/download/v${XCADDY_VERSION}/xcaddy_${XCADDY_VERSION}_linux_amd64.tar.gz" -O - | tar -xz \
    && ./xcaddy build ${VERSION} \
    --with github.com/caddy-dns/cloudflare \
    --with github.com/caddyserver/replace-response


FROM alpine:latest

COPY --chmod=0755 --from=0 /tmp/xcaddy/caddy /usr/bin/caddy

RUN set -eux \
    ; apk add --no-cache ca-certificates mailcap libcap \
    ; mkdir -p /config/caddy /data/caddy /etc/caddy /usr/share/caddy

ENV XDG_CONFIG_HOME /config
ENV XDG_DATA_HOME /data

EXPOSE 80
EXPOSE 443
EXPOSE 443/udp
EXPOSE 2019

CMD ["caddy", "run", "--config", "/etc/caddy/Caddyfile", "--adapter", "caddyfile"]
