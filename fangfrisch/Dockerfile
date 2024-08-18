FROM python:3-alpine AS builder
LABEL org.opencontainers.image.authors="Alexander Turcic <alexander@pixel-plus.ch>"

RUN apk add --update --no-cache --virtual .build-deps gcc libffi-dev musl-dev \
    && python -m venv /app/venv \
    && /app/venv/bin/pip install --no-cache-dir fangfrisch==1.9.0 \
    && apk del .build-deps

FROM python:3-alpine

ARG USER_ID=100
ARG GROUP_ID=101
RUN addgroup -g ${GROUP_ID} clamav && \
    adduser -D -u ${USER_ID} -G clamav clamav

COPY --from=builder --chown=clamav:clamav /app/venv /app/venv

RUN mkdir /var/lib/fangfrisch \
    && chown -R clamav:clamav /var/lib/fangfrisch

RUN apk add --update --no-cache supercronic && \
    rm -rf /var/cache/apk/*

USER clamav

ENV PATH="/app/venv/bin:$PATH"
WORKDIR /app

ENTRYPOINT ["supercronic", "/etc/crontab"]
