FROM alpine:latest

ARG VERSION='tuic-server-1.0.0'

RUN set -eux \
    ; apk add --no-cache ca-certificates \
    ; mkdir -p /etc/tuic \
    ; wget -P /usr/bin/ -O /usr/bin/tuic-server "https://github.com/EAimTY/tuic/releases/download/${VERSION}/${VERSION}-x86_64-unknown-linux-musl" \
    && chmod +x /usr/bin/tuic-server

CMD [ "/usr/bin/tuic-server", "-c","/etc/tuic/tuic-server.json" ]
