FROM alpine:{{alpine_version}}

RUN apk add --no-cache --update wireguard-tools

ENTRYPOINT [ "/etc/wireguard/util/wg-startup.sh" ]
