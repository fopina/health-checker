FROM golang:1.14-alpine as builder

ARG VERSION="dev"
ADD . /app
WORKDIR /app
RUN go build -ldflags="-s -w -X main.VERSION=${VERSION}" -o health-checker

FROM alpine:3.11 as bash

RUN apk add --no-cache bash

COPY --from=builder /app/health-checker /usr/bin/health-checker
ENTRYPOINT [ "/usr/bin/health-checker" ]

FROM python:3.7-alpine as python

RUN apk add --no-cache bash

COPY --from=builder /app/health-checker /usr/bin/health-checker
ENTRYPOINT [ "/usr/bin/health-checker" ]
