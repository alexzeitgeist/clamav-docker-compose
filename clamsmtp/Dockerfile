FROM golang:alpine AS builder

ENV CGO_ENABLED=0

RUN go install -ldflags="-s -w" github.com/alexzeitgeist/clamaction/cmd/clamaction@v1.0.2

FROM alpine:3.20
LABEL org.opencontainers.image.authors="Alexander Turcic <alexander@pixel-plus.ch>"

RUN apk add --update --no-cache clamsmtp && \
    rm -rf /var/cache/apk/*

RUN  mkdir /var/spool/clamsmtp && \
    chown clamav:clamav /var/spool/clamsmtp && \
    chmod 750 /var/spool/clamsmtp

RUN  mkdir /var/spool/quarantine && \
    chown clamav:clamav /var/spool/quarantine && \
    chmod 750 /var/spool/quarantine

COPY --from=builder --chown=clamav:clamav --chmod=750 /go/bin/clamaction /usr/bin/clamaction

CMD ["/usr/sbin/clamsmtpd", "-d 2"]
