FROM alpine:edge
MAINTAINER Alexander Grynchuk
RUN apk add --no-cache -X http://dl-cdn.alpinelinux.org/alpine/edge/testing i2pd
USER i2pd
ENTRYPOINT ["/usr/sbin/i2pd", \
            "--http.enabled=true", "--http.address=0.0.0.0", \
            "--httpproxy.enabled=true", "--httpproxy.address=0.0.0.0", \
            "--socksproxy.enabled=false"]
CMD ["console"]