# source https://github.com/danielguerra69/alpine-sdk
FROM alpine:3.10 AS alpine-sdk
MAINTAINER Daniel Guerra
#meta container, we want fresh builds
ONBUILD RUN apk update
ONBUILD RUN apk add alpine-sdk
ONBUILD RUN addgroup sdk
ONBUILD RUN adduser  -G sdk -s /bin/sh -D sdk
ONBUILD RUN echo "sdk:sdk"| /usr/sbin/chpasswd
ONBUILD RUN echo "sdk    ALL=(ALL) ALL" >> /etc/sudoers
ONBUILD RUN chmod g+w /var/cache/distfiles/
ONBUILD RUN sudo addgroup sdk abuild
ONBUILD USER sdk
ONBUILD WORKDIR /tmp
ONBUILD RUN git clone --recursive https://github.com/alpinelinux/aports.git
ONBUILD WORKDIR /home/sdk

# source https://github.com/danielguerra69/alpine-i2pd/
FROM alpine-sdk as builder
MAINTAINER Daniel Guerra
RUN echo "sdk" | sudo  -S adduser -s /bin/false -D i2pd
WORKDIR /tmp/aports/testing/i2pd
RUN abuild-keygen -a -n
RUN abuild fetch
RUN abuild unpack
RUN abuild deps
RUN abuild prepare
RUN abuild build
RUN abuild rootpkg

FROM alpine:3.10
MAINTAINER Daniel Guerra
RUN apk add --update --no-cache sudo boost
COPY --from=builder /home/sdk/.abuild /tmp/.abuild
RUN find /tmp/.abuild -name "*.pub" -exec cp {} /etc/apk/keys \;
COPY --from=builder /home/sdk/packages/testing/x86_64/i2pd-2.29.0-r1.apk /tmp/i2pd-2.29.0-r1.apk
RUN apk --no-cache add /tmp/i2pd-2.29.0-r1.apk
RUN mkdir -p /var/lib/i2pd/.i2pd
RUN ln -s /var/lib/i2pd/certificates /var/lib/i2pd/.i2pd/certificates
RUN chown  -R i2pd:i2pd /var/lib/i2pd
USER i2pd
ENTRYPOINT ["/usr/sbin/i2pd"]
CMD ["console"]