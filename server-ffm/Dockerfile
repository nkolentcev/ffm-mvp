FROM golang:1.21.4-alpine3.18 AS builder
WORKDIR /usr/local/src
RUN apk add --no-cache bash git make gcc gettext musl-dev
COPY ["app/go.mod", "./"]
RUN go mod download
COPY app ./
RUN go build -o ./bin/ffm cmd/ffm/main.go
FROM alpine
COPY --from=builder /usr/local/src/bin/ffm /
COPY configs/local.yaml /config.yaml
CMD ["/ffm"]