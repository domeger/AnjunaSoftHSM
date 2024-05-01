FROM alpine:3.8

ARG SOFTHSM2_VERSION=2.5.0

ENV SOFTHSM2_VERSION=${SOFTHSM2_VERSION} \
    SOFTHSM2_SOURCES=/tmp/softhsm2 \
    SOFTHSM2_CONF=/etc/softhsm2.conf \
    SOFTHSM2_TOKEN_LABEL="my-token" \
    SOFTHSM2_TOKEN_PIN="1234" \
    SOFTHSM2_TOKEN_SO_PIN="1234"

# install build dependencies
RUN apk --update add \
    alpine-sdk \
    autoconf \
    automake \
    git \
    libtool \
    openssl-dev

# build and install SoftHSM2
RUN git clone https://github.com/opendnssec/SoftHSMv2.git ${SOFTHSM2_SOURCES}
WORKDIR ${SOFTHSM2_SOURCES}
RUN git checkout ${SOFTHSM2_VERSION} -b ${SOFTHSM2_VERSION} \
    && sh autogen.sh \
    && ./configure --prefix=/usr/local \
    && make \
    && make install

WORKDIR /root
RUN rm -fr ${SOFTHSM2_SOURCES}

# install pkcs11-tool
RUN apk --update add opensc

# create token directory and configure SoftHSM2
RUN mkdir -p /var/lib/softhsm/tokens
RUN echo "directories.tokendir = /var/lib/softhsm/tokens" > $SOFTHSM2_CONF
RUN echo "objectstore.backend = file" >> $SOFTHSM2_CONF
RUN echo "log.level = INFO" >> $SOFTHSM2_CONF
RUN echo "slots.removable = false" >> $SOFTHSM2_CONF

# initialize token
RUN softhsm2-util --init-token --slot 0 --label $SOFTHSM2_TOKEN_LABEL --pin $SOFTHSM2_TOKEN_PIN --so-pin $SOFTHSM2_TOKEN_SO_PIN

EXPOSE 5657

CMD ["softhsm2-util", "--show-slots"]