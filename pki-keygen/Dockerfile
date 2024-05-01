FROM alpine:3.8

RUN apk --update add \
    openssl \
    opensc

ENV SOFTHSM2_CONF=/etc/softhsm2.conf \
    SOFTHSM2_SERVER_IP="softhsm-container" \
    SOFTHSM2_SERVER_PORT="5657" \
    SOFTHSM2_TOKEN_PIN="1234"

RUN echo "directories.tokendir = /var/lib/softhsm/tokens" > $SOFTHSM2_CONF
RUN echo "objectstore.backend = pkcs11" >> $SOFTHSM2_CONF
RUN echo "slots.removable = false" >> $SOFTHSM2_CONF
RUN echo "pkcs11.library = /usr/lib/softhsm/libsofthsm2.so" >> $SOFTHSM2_CONF
RUN echo "pkcs11.module = /usr/lib/softhsm/libsofthsm2.so" >> $SOFTHSM2_CONF
RUN echo "pkcs11.module.path = /usr/lib/softhsm/libsofthsm2.so" >> $SOFTHSM2_CONF

CMD ["sh", "-c", "pkcs11-tool --module tcp://$SOFTHSM2_SERVER_IP:$SOFTHSM2_SERVER_PORT --login --pin $SOFTHSM2_TOKEN_PIN --keypairgen --key-type rsa:2048 --label my-key"]