# wgcf-docker

CloudFlare WARP in docker

Credits: https://github.com/Neilpang/wgcf-docker

## Run a single container:

```
docker run --rm -it \
    --name wgcf \
    --sysctl net.ipv6.conf.all.disable_ipv6=0 \
    --privileged --cap-add net_admin \
    -v /lib/modules:/lib/modules \
    -v $(pwd)/wgcf:/wgcf \
    kenhv/wgcf
```

The above command will enable both IPv4 and IPv6, you can enable IPv4 or IPv6 only like following:

### Enable IPv4 only:

```
docker run --rm -it \
    --name wgcf \
    --sysctl net.ipv6.conf.all.disable_ipv6=0 \
    --privileged --cap-add net_admin \
    -v /lib/modules:/lib/modules \
    -v $(pwd)/wgcf:/wgcf \
    kenhv/wgcf -4
```

### Enable IPv6 only:

```
docker run --rm -it \
    --name wgcf \
    --sysctl net.ipv6.conf.all.disable_ipv6=0 \
    --privileged --cap-add net_admin \
    -v /lib/modules:/lib/modules \
    -v $(pwd)/wgcf:/wgcf \
    kenhv/wgcf -6
```

### If another container needs to use the wgcf network, run it like:

```

docker run --rm  -it  --network container:wgcf  curlimages/curl curl ipinfo.io

```

## Docker compose example:

### Enable both IPv4 and IPv6 by default:

```
version: "2.4"
services:
  wgcf:
    image: kenhv/wgcf:latest
    volumes:
      - ./wgcf:/wgcf
      - /lib/modules:/lib/modules
    privileged: true
    sysctls:
      net.ipv6.conf.all.disable_ipv6: 0
    cap_add:
      - NET_ADMIN

  test:
    image: curlimages/curl
    network_mode: "service:wgcf"
    depends_on:
      - wgcf
    command: curl ipinfo.io
```

### Enable IPv4 only:

```
version: "2.4"
services:
  wgcf:
    image: kenhv/wgcf:latest
    volumes:
      - ./wgcf:/wgcf
      - /lib/modules:/lib/modules
    privileged: true
    sysctls:
      net.ipv6.conf.all.disable_ipv6: 0
    cap_add:
      - NET_ADMIN
    command: "-4"

  test:
    image: curlimages/curl
    network_mode: "service:wgcf"
    depends_on:
      - wgcf
    command: curl ipinfo.io
```

### Enable IPv6 only:

```
version: "2.4"
services:
  wgcf:
    image: kenhv/wgcf:latest
    volumes:
      - ./wgcf:/wgcf
      - /lib/modules:/lib/modules
    privileged: true
    sysctls:
      net.ipv6.conf.all.disable_ipv6: 0
    cap_add:
      - NET_ADMIN
    command: "-6"

  test:
    image: curlimages/curl
    network_mode: "service:wgcf"
    depends_on:
      - wgcf
    command: curl ipv6.ip.sb
```
