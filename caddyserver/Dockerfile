FROM golang:1.12.9-buster as builder

ENV GO111MODULE=on
ENV CGO_ENABLED=0
ENV GOOS=linux
RUN go get github.com/caddyserver/caddy/caddy
RUN which caddy


FROM alpine:3.10

COPY --from=builder /go/bin/caddy /usr/sbin/caddy
# Validate install
RUN /usr/sbin/caddy -version

EXPOSE 80 443

VOLUME ["/var/www/html","/etc/Caddyfile"]

WORKDIR /var/www/html
ENTRYPOINT ["/usr/sbin/caddy"]
CMD ["--conf", "/etc/Caddyfile","--log","stdout","--agree=true"]
