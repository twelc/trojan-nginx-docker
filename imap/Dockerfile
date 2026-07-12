FROM alpine:latest as builder 

WORKDIR /opt/build

RUN apk update && apk upgrade
RUN apk add git go

RUN git clone "https://github.com/noiseonwires/true-imap-tunnel.git"

WORKDIR /opt/build/true-imap-tunnel

RUN go build -trimpath -o /app/true-imap-tunnel ./cmd/true-imap-tunnel

FROM alpine:latest

WORKDIR /app
COPY --from=builder /app/true-imap-tunnel /app/true-imap-tunnel
COPY ./config.yaml /app/config.yaml

ENTRYPOINT [ "/app/true-imap-tunnel", "-config", "/app/config.yaml"]