FROM alpine:latest

COPY entry.sh /entry.sh

RUN apk update -f \
  && apk --no-cache add -f \
  curl ca-certificates \
  iproute2 net-tools iptables \
  wireguard-tools openresolv \
  && rm -rf /var/cache/apk/* \
  && curl -fsSL git.io/wgcf.sh | bash \
  && mkdir -p /wgcf \
  && chmod +x /entry.sh

WORKDIR /wgcf
VOLUME /wgcf

ENTRYPOINT ["/entry.sh"]

# vim: ft=dockerfile
