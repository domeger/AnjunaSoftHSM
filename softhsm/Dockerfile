FROM alpine:latest

ENV SOFTHSM2_CONF=/etc/softhsm2.conf
ENV SOFTHSM2_TOKEN_LABEL="my-token"
ENV SOFTHSM2_TOKEN_PIN="1234"
ENV SOFTHSM2_TOKEN_SO_PIN="1234"

RUN apk add --no-cache softhsm

RUN mkdir -p /var/lib/softhsm/tokens

RUN echo "directories.tokendir = /var/lib/softhsm/tokens" > $SOFTHSM2_CONF
RUN echo "objectstore.backend = file" >> $SOFTHSM2_CONF
RUN echo "log.level = INFO" >> $SOFTHSM2_CONF
RUN echo "slots.removable = false" >> $SOFTHSM2_CONF

RUN softhsm2-util --init-token --slot 0 --label $SOFTHSM2_TOKEN_LABEL --pin $SOFTHSM2_TOKEN_PIN --so-pin $SOFTHSM2_TOKEN_SO_PIN

EXPOSE 5657

CMD ["softhsm2-util", "--show-slots"]